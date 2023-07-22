<template>
  <div class="text-center text-[28px] mb-4 font-bold">注册</div>

  <div class="px-6 pb-2">
    <TextInput
      placeholder="用户名"
      v-model:input="name"
      inputType="text"
      :autoFocus="true"
      :error="errors && errors.name ? errors.name[0] : ''"
    />
  </div>

  <div class="px-6 pb-2">
    <TextInput
      placeholder="电子邮箱"
      v-model:input="email"
      inputType="email"
      :error="errors && errors.email ? errors.email[0] : ''"
    />
  </div>

  <div class="px-6 pb-2">
    <TextInput
      placeholder="密码"
      v-model:input="password"
      inputType="password"
      :error="errors && errors.password ? errors.password[0] : ''"
    />
  </div>

  <div class="px-6 pb-2">
    <TextInput
      placeholder="确认密码"
      v-model:input="confirmPassword"
      inputType="password"
      :error="errors && errors.confirmPassword ? errors.confirmPassword[0] : ''"
    />
  </div>

  <div class="px-6 pb-2 mt-6">
    <button
      :disabled="!name || !email || !password || !confirmPassword"
      :class="
        !name || !email || !password || !confirmPassword
          ? 'bg-gray-200'
          : 'bg-[#F02C56]'
      "
      @click="register()"
      class="w-full text-[17px] font-semibold text-white py-3 rounded-sm"
    >
      注册
    </button>
  </div>
</template>

<script setup>
const { $userStore, $generalStore } = useNuxtApp();

let name = ref(null);
let email = ref(null);
let password = ref(null);
let confirmPassword = ref(null);
let errors = ref(null);

const register = async () => {
  errors.value = null;

  try {
    await $userStore.getTokens();
    await $userStore.register(
      name.value,
      email.value,
      password.value,
      confirmPassword.value
    );
    await $userStore.getUser();
    await $generalStore.getRandomUsers("suggested");
    await $generalStore.getRandomUsers("following");

    $generalStore.isLoginOpen = false;
  } catch (error) {
    errors.value = error.response.data.errors;
  }
};
</script>
