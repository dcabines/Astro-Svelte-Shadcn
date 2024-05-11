<script lang="ts">
  import type { HTMLAttributes } from "svelte/elements";
  import { cn } from "$lib/utils.js";
  import * as util from '$lib/utils';

  import BellRing from "lucide-svelte/icons/bell-ring";
  import Check from "lucide-svelte/icons/check";
  import { Button } from "$lib/components/ui/button/index.js";
  import { Switch } from "$lib/components/ui/switch/index.js";
  import { Calendar } from "$lib/components/ui/calendar/index.js";
  import CalendarIcon from "lucide-svelte/icons/calendar";

  import * as Card from "$lib/components/ui/card/index.js";
  import * as Popover from "$lib/components/ui/popover/index.js";

  import PocketBase from 'pocketbase';

  const url = 'https://problem-some.pockethost.io/'
  const client = new PocketBase(url);
  let records = util.getPeople(client);

  import {
    DateFormatter,
    type DateValue,
    getLocalTimeZone,
  } from "@internationalized/date";

  const df = new DateFormatter("en-US", {
    dateStyle: "long",
  });

  let value: DateValue | undefined = undefined;
  let checked: boolean = true;
  let isDark: boolean = false;

  function loadPeople() {
    records = util.getPeople(client);
  }

  function toggleDark() {
    isDark = !isDark;
    if (isDark) document.body.classList.add('dark');
    if (!isDark) document.body.classList.remove('dark');
  }

  type $$Props = HTMLAttributes<HTMLDivElement>;
  let className: $$Props["class"] = undefined;
  export { className as class };
</script>

{#await records}
<span>Loading...</span>
{:then people}
<Card.Root class={cn("w-[380px]", className)}>
  <Card.Header>
    <Card.Title>Notifications</Card.Title>
    <Card.Description>You have 3 unread messages.</Card.Description>
  </Card.Header>
  <Card.Content class="grid gap-4">
    <Popover.Root>
      <Popover.Trigger asChild let:builder>
        <Button
          variant="outline"
          class={cn(
            "w-[280px] justify-start text-left font-normal",
            !value && "text-muted-foreground",
          )}
          builders={[builder]}
        >
          <CalendarIcon class="mr-2 h-4 w-4" />
          {value ? df.format(value.toDate(getLocalTimeZone())) : "Pick a date"}
        </Button>
      </Popover.Trigger>
      <Popover.Content class="w-auto p-0">
        <Calendar bind:value initialFocus />
      </Popover.Content>
    </Popover.Root>

    <div class="flex items-center space-x-4 rounded-md border p-4">
      <BellRing />
      <div class="flex-1 space-y-1">
        <p class="text-sm font-medium leading-none">Push Notifications</p>
        <p class="text-sm text-muted-foreground">
          Send notifications to device.
        </p>
      </div>
      <Switch bind:checked />
    </div>
    <div>
      {#each people as person, idx (idx)}
        <div
          class="mb-4 grid grid-cols-[25px_1fr] items-start pb-4 last:mb-0 last:pb-0"
        >
          <span class="flex h-2 w-2 translate-y-1 rounded-full bg-sky-500" />
          <div class="space-y-1">
            <p class="text-sm font-medium leading-none">
              {person.name}
            </p>
            <p class="text-sm text-muted-foreground">
              {@html person.bio}
            </p>
          </div>
        </div>
      {/each}
    </div>
  </Card.Content>
  <Card.Footer class="flex flex-col gap-1">
    <Button on:click={toggleDark} class="w-full">
      <Check class="mr-2 h-4 w-4" /> Mark all as read
    </Button>
    <Button on:click={loadPeople} class="w-full">
      <Check class="mr-2 h-4 w-4" /> Reload
    </Button>
  </Card.Footer>
</Card.Root>
{:catch error}
  <pre>{error}</pre>
{/await}