<template>
  <h1 class="user-name">Информация о пользователе "{{ data.name }}"</h1>
  <table class="table table-striped">
    <thead>
      <tr>
        <th>Ключ</th>
        <th>Значення</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(value, key) in data" :key="key">
        <td>{{ key }}</td>
        <td>{{ value }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
    }
  },
};
</script>