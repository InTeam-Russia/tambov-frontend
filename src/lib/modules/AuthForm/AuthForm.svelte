<script lang="ts">
  import { Button } from '$lib/components/ui/button';
  import { Input } from '$lib/components/ui/input';
  import { Label } from '$lib/components/ui/label';
  import { Eye, EyeOff } from 'lucide-svelte';
  import type { FormState, FormErrors } from './types';

  let formState: FormState = {
    email: '',
    password: '',
  };

  let showPassword: boolean = false;
  let errors: FormErrors = {};

  const validateEmail = (email: string): boolean => {
    const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return regex.test(email);
  };

  const handleSubmit: (arg0: SubmitEvent) => void = (event: SubmitEvent) => {
    event.preventDefault();
    errors = {};

    if (!formState.email) {
      errors.email = 'Электронная почта обязательна';
    } else if (!validateEmail(formState.email)) {
      errors.email = 'Введите корректный адрес электронной почты';
    }

    if (!formState.password) {
      errors.password = 'Пароль обязателен';
    }

    if (Object.keys(errors).length > 0) {
      return;
    }

    // TODO: Отправка данных на сервер (заглушка)
    console.log('Отправка данных на сервер:', formState);
  };
</script>

<div class="max-w-md mx-auto p-6 bg-white dark:bg-zinc-900 rounded-lg shadow-md">
  <h2 class="text-2xl font-bold text-center mb-4">Авторизация</h2>

  <form on:submit={handleSubmit}>
    <div class="mb-4">
      <Label for="email">Электронная почта</Label>
      <Input
        type="text"
        id="email"
        bind:value={formState.email}
        placeholder="Электронная почта"
        class="mt-1" />
      {#if errors.email}
        <p class="text-red-500 text-sm">{errors.email}</p>
      {/if}
    </div>

    <div class="mb-4 relative">
      <Label for="password">Пароль</Label>
      <Input
        type={showPassword ? 'text' : 'password'}
        id="password"
        bind:value={formState.password}
        placeholder="Пароль"
        class="mt-1" />
      {#if errors.password}
        <p class="text-red-500 text-sm">{errors.password}</p>
      {/if}
      <button
        type="button"
        on:click={() => (showPassword = !showPassword)}
        class="absolute right-2 top-10">
        {#if showPassword}
          <Eye class="w-5 h-5 text-gray-500" />
        {:else}
          <EyeOff class="w-5 h-5 text-gray-500" />
        {/if}
      </button>
    </div>

    <Button
      type="submit"
      variant="default"
      class="w-full py-2 mt-4">
      Войти
    </Button>
  </form>

  <p class="mt-4 text-center text-sm">
    Нет аккаунта?
    <a
      href="/register"
      class="text-blue-600 hover:underline">Зарегистрироваться</a>
  </p>
</div>
