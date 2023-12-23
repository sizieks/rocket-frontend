<template>
  <a-card title="Тестовое задание">
    <template #extra>
      <a-input-search
        allowClear
        v-model:value="inputSearch"
        placeholder="Найти..."
        id="input-query"
        class="input-search"
        @search="$emit('search', inputSearch)"
      />
    </template>
    <a-table
      :dataSource="dataSource"
      :pagination="pagination"
      :columns="columns"
      :rowKey="(record: ILead) => record.id"
      :loading="loading"
      sticky
      expandRowByClick
    >
      <template #expandedRowRender="{ record }">
        <a-flex align="center" gap="small" class="contact-row">
          <a-avatar :size="24">
            <template #icon><user-outlined /></template>
          </a-avatar>
          {{ record.contact_name }}
          <a-flex gap="middle" class="contact-box">
            <a :href="`tel:${record.contact_phone}`"><phone-outlined /></a>
            <a :href="`mailto:${record.contact_email}`"><mail-outlined /></a>
          </a-flex>
        </a-flex>
      </template>
      <template #bodyCell="{ column, record }">
        <template v-if="column.key === 'price'">
          {{ record.price.toLocaleString() }}
        </template>
        <template v-if="column.key === 'status_name'">
          <a-tag :color="record.status_color" class="lead-status">
            {{ record.status_name }}
          </a-tag>
        </template>
        <template v-if="column.key === 'user'">
          <a-avatar :size="24" class="userpic">
            <template #icon><user-outlined /></template>
          </a-avatar>
          {{ record.user }}
        </template>
        <template v-if="column.key === 'created_at'">
          {{ formatDate(record.created_at) }}
        </template>
      </template>
      <template #expandColumnTitle />
    </a-table>
  </a-card>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue';
import { ILead } from '../types';
import {
  MailOutlined,
  PhoneOutlined,
  UserOutlined,
} from '@ant-design/icons-vue';

const props = defineProps<{
  dataSource: ILead[];
  loading: boolean;
}>();

const inputSearch = ref('');

const columns = [
  {
    title: 'Название',
    dataIndex: 'name',
    key: 'name',
  },
  {
    title: 'Бюджет',
    dataIndex: 'price',
    key: 'price',
    sorter: {
      compare: (a: ILead, b: ILead) => a.price - b.price,
    },
  },
  {
    title: 'Статус',
    dataIndex: 'status_name',
    key: 'status_name',
    sorter: {
      compare: (a: ILead, b: ILead) =>
        a.status_name.localeCompare(b.status_name),
    },
  },
  {
    title: 'Ответственный',
    dataIndex: 'user',
    key: 'user',
    sorter: {
      compare: (a: ILead, b: ILead) => a.user.localeCompare(b.user),
    },
  },
  {
    title: 'Дата создания',
    dataIndex: 'created_at',
    key: 'created_at',
    sorter: {
      compare: (a: ILead, b: ILead) => a.created_at.localeCompare(b.created_at),
    },
  },
];

const current = ref(1);
const size = ref(20);

const pagination = computed(() => ({
  total: props.dataSource.length,
  current: current.value,
  pageSize: size.value,
  onChange: (page: number, pageSize: number) => {
    current.value = page;
    size.value = pageSize;
  },
}));

const formatDate = (
  date: string,
  options: Intl.DateTimeFormatOptions = {
    year: 'numeric',
    month: 'numeric',
    day: 'numeric',
    hour: 'numeric',
    minute: 'numeric',
  }
): string => {
  // undefined to use the browser's default locale
  return new Intl.DateTimeFormat(undefined, options).format(new Date(date));
};
</script>

<style scoped>
.input-search {
  width: 200px;
}

.contact-row {
  width: 240px;
  margin-left: 48px;
}

.contact-box {
  margin-left: auto;
}

.lead-status {
  color: rgba(0, 0, 0, 0.88);
}

.userpic {
  background-color: rgb(24, 144, 255);
  margin-right: 8px;
}
</style>
