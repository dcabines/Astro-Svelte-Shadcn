<script lang="ts">
  import Login from "$lib/components/my-login.svelte";
  import Settings from "$lib/components/my-settings.svelte";
  import Page from "$lib/components/my-page.svelte";
  import Notifications from "$lib/components/my-card.svelte";
  import JokeTax from "$lib/components/joke-tax.svelte";
  import * as Tabs from "$lib/components/ui/tabs/index.js";
  import ModeSwitch from '$lib/components/mode-switch.svelte';
</script>

<Tabs.Root class="h-full" value="week">
  <div class="flex items-center">
    <Tabs.List>
      <Tabs.Trigger value="week">Login</Tabs.Trigger>
      <Tabs.Trigger value="month">Settings</Tabs.Trigger>
      <Tabs.Trigger value="year">Page</Tabs.Trigger>
      <Tabs.Trigger value="Notifications">Notifications</Tabs.Trigger>
      <Tabs.Trigger value="JokeTax">JokeTax</Tabs.Trigger>
      <Tabs.Trigger value="ModeSwitch">ModeSwitch</Tabs.Trigger>
    </Tabs.List>
  </div>
  <Tabs.Content value="week" class="h-full">
    <Login />
  </Tabs.Content>
  <Tabs.Content value="month" class="h-full">
    <Settings />
  </Tabs.Content>
  <Tabs.Content value="year" class="h-full">
    <Page />
  </Tabs.Content>
  <Tabs.Content value="Notifications" class="h-full">
    <Notifications />
  </Tabs.Content>
  <Tabs.Content value="JokeTax" class="h-full">
    <JokeTax />
  </Tabs.Content>
  <Tabs.Content value="ModeSwitch" class="h-full">
    <ModeSwitch />
  </Tabs.Content>
</Tabs.Root>
