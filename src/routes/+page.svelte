<script lang="ts">
  import { OTPInput, OTPRoot } from '@jimmyverburgt/svelte-input-otp';
  import Minus from 'lucide-svelte/icons/minus';
  import Dot from 'lucide-svelte/icons/dot';
  import Search from 'lucide-svelte/icons/search';
  import {
    Card,
    CardContent,
    CardDescription,
    CardFooter,
    CardHeader,
    CardTitle,
  } from '$lib/components/ui/card';
  import { Button } from '$lib/components/ui/button';
  import CircleAlert from 'lucide-svelte/icons/circle-alert';
  import * as Alert from '$lib/components/ui/alert/index.js';
  import { goto } from '$app/navigation';

  let otpref: any;

  // Set start value
  let value = '';
  let error = false;

  const checkInn: boolean = (inn: string) => {
    if (!(!isNaN(inn) && inn.length == 10 && Number(inn) > 0)) {
      return false;
    }
    return true;
    //return ((2 * inn[0] + 4 * inn[1] + 10 * inn[2] + 3 * inn[3] + 5 * inn[4] + 9 * inn[5] + 4 * inn[6] + 6 * inn[7] + 8 * inn[8]) % 11) % 10 == inn[0]
  };

  function handleOtpComplete(otp: string) {
    error = !checkInn(otp);
  }

  function handleOtpChange(event: { detail: string }) {
    console.log('OTP changed:', value);
  }

  const loadOrganisation = () => {
    error = !checkInn(value);
    if (error) {
      return;
    }
    goto('organisation/' + value);
  };
</script>

<section class="main-section">
  <Card>
    <CardHeader>
      <CardTitle class="text-4xl">Поиск по ИНН</CardTitle>
      <CardDescription
        >Чтобы получить информацию об организации, введите её ИНН в поле ниже:</CardDescription>
    </CardHeader>
    <CardContent>
      {#if error}
        <Alert.Root
          variant="destructive"
          class="mb-8 transition-all">
          <CircleAlert class="h-4 w-4" />
          <Alert.Title>Ошибка</Alert.Title>
          <Alert.Description>Это не похоже на ИНН. Проверьте его правильность.</Alert.Description>
        </Alert.Root>
      {/if}
      <OTPRoot
        bind:this={otpref}
        maxLength={10}
        on:change={handleOtpChange}
        bind:value
        autoFocus={true}
        onComplete={handleOtpComplete}
        className="flex items-center gap-2"
        inputMode="numeric"
        ariaLabel="Svelte OTP Code">
        <div class="flex items-center">
          <OTPInput
            index={0}
            className="input-number relative flex items-center justify-center border-y border-r border-input text-xl transition-all first:rounded-l-md first:border-l last:rounded-r-md"
            focusClassName="z-10 ring-2 ring-ring ring-offset-background" />
          <OTPInput
            index={1}
            className="input-number relative flex items-center justify-center border-y border-r border-input text-xl transition-all first:rounded-l-md first:border-l last:rounded-r-md"
            focusClassName="z-10 ring-2 ring-ring ring-offset-background" />
          <OTPInput
            index={2}
            className="input-number relative flex items-center justify-center border-y border-r border-input text-xl transition-all first:rounded-l-md first:border-l last:rounded-r-md"
            focusClassName="z-10 ring-2 ring-ring ring-offset-background" />
          <OTPInput
            index={3}
            className="input-number relative flex items-center justify-center border-y border-r border-input text-xl transition-all first:rounded-l-md first:border-l last:rounded-r-md"
            focusClassName="z-10 ring-2 ring-ring ring-offset-background" />
        </div>
        <div class="mx-1">
          <Dot />
        </div>
        <div class="flex items-center">
          <OTPInput
            index={4}
            className="input-number relative flex items-center justify-center border-y border-r border-input text-xl transition-all first:rounded-l-md first:border-l last:rounded-r-md"
            focusClassName="z-10 ring-2 ring-ring ring-offset-background" />
          <OTPInput
            index={5}
            className="input-number relative flex items-center justify-center border-y border-r border-input text-xl transition-all first:rounded-l-md first:border-l last:rounded-r-md"
            focusClassName="z-10 ring-2 ring-ring ring-offset-background" />
          <OTPInput
            index={6}
            className="input-number relative flex items-center justify-center border-y border-r border-input text-xl transition-all first:rounded-l-md first:border-l last:rounded-r-md"
            focusClassName="z-10 ring-2 ring-ring ring-offset-background" />
          <OTPInput
            index={7}
            className="input-number relative flex items-center justify-center border-y border-r border-input text-xl transition-all first:rounded-l-md first:border-l last:rounded-r-md"
            focusClassName="z-10 ring-2 ring-ring ring-offset-background" />
          <OTPInput
            index={8}
            className="input-number relative flex items-center justify-center border-y border-r border-input text-xl transition-all first:rounded-l-md first:border-l last:rounded-r-md"
            focusClassName="z-10 ring-2 ring-ring ring-offset-background" />
        </div>
        <div class="mx-1">
          <Dot />
        </div>
        <div class="flex items-center">
          <OTPInput
            index={9}
            className="input-number relative flex items-center justify-center border-y border-r border-input text-xl transition-all first:rounded-l-md first:border-l last:rounded-r-md"
            focusClassName="z-10 ring-2 ring-ring ring-offset-background" />
        </div>
      </OTPRoot>
    </CardContent>
    <CardFooter class="flex justify-end">
      <Button
        class="flex flex-row items-center"
        on:click={loadOrganisation}><Search class="mr-2 h-4 w-4" />&nbsp;Найти</Button>
    </CardFooter>
  </Card>
</section>

<style>
  .main-section {
    height: calc(100vh - 56px);
    width: 100vw;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }
  :global(.input-number) {
    width: 3rem;
    height: 4rem;
  }
</style>
