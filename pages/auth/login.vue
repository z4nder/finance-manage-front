<template>
  <NuxtLayout :name="layout">
    <div class="bg-white py-8 px-4 shadow sm:rounded-lg sm:px-10">
      <div class="flex justify-center text-center items-center text-red-500">
        {{ errors?.general }}
      </div>
      <form class="space-y-6" @submit.prevent="submit">
        <v-input
          id="email"
          v-model="form.email"
          :value="form.email"
          :error="errors?.email"
          class="mt-10"
          label="Email"
          type="email"
        />
        <v-input
          id="password"
          v-model="form.password"
          :value="form.password"
          :error="errors?.password"
          class="mt-10"
          label="Senha"
          type="password"
        />
        <div>
          <v-button type="submit">Entrar</v-button>
        </div>
      </form>
      <div class="mt-6">
        <div class="relative">
          <div class="absolute inset-0 flex items-center">
            <div class="w-full border-t border-gray-300" />
          </div>
          <div class="relative flex justify-center text-sm">
            <span class="px-2 bg-white text-gray-500">
              Ainda não possui uma conta ?
              <v-a href="/auth/register">Cria uma conta</v-a>
            </span>
          </div>
        </div>
      </div>
    </div>
  </NuxtLayout>
</template>

<script setup lang="ts">
import { reactive } from "vue";
const { login, errors } = useAuth();

definePageMeta({ middleware: ["guest"] });
const layout = "guest";

const form = reactive({
  email: "",
  password: "",
});

const submit = async () => {
  await login(form);
};
</script>
