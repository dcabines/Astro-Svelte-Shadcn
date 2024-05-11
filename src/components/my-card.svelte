<script lang="ts">
  import type { HTMLAttributes } from "svelte/elements";
  import { cn } from "$lib/utils.js";

  import BellRing from "lucide-svelte/icons/bell-ring";
  import Check from "lucide-svelte/icons/check";
  import { Button } from "$lib/components/ui/button/index.js";
  import { Switch } from "$lib/components/ui/switch/index.js";
  import { Calendar } from "$lib/components/ui/calendar/index.js";
  import CalendarIcon from "lucide-svelte/icons/calendar";

  import * as Card from "$lib/components/ui/card/index.js";
  import * as Popover from "$lib/components/ui/popover/index.js";

  import {
    DateFormatter,
    type DateValue,
    getLocalTimeZone,
  } from "@internationalized/date";

  const notifications = [
    {
      title: "Your call has been confirmed.",
      description: "1 hour ago",
    },
    {
      title: "You have a new message!",
      description: "1 hour ago",
    },
    {
      title: "Your subscription is expiring soon!",
      description: "2 hours ago",
    },
  ];

  const df = new DateFormatter("en-US", {
    dateStyle: "long",
  });

  let value: DateValue | undefined = undefined;
  let checked: boolean = true;

  type $$Props = HTMLAttributes<HTMLDivElement>;
  let className: $$Props["class"] = undefined;
  export { className as class };
</script>

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
      <div>{checked}</div>
    </div>
    <div>
      {#each notifications as notification, idx (idx)}
        <div
          class="mb-4 grid grid-cols-[25px_1fr] items-start pb-4 last:mb-0 last:pb-0"
        >
          <span class="flex h-2 w-2 translate-y-1 rounded-full bg-sky-500" />
          <div class="space-y-1">
            <p class="text-sm font-medium leading-none">
              {notification.title}
            </p>
            <p class="text-sm text-muted-foreground">
              {notification.description}
            </p>
          </div>
        </div>
      {/each}
    </div>
  </Card.Content>
  <Card.Footer>
    <Button
      data-confetti-button
      on:click={() => alert("clicked")}
      class="w-full"
    >
      <Check class="mr-2 h-4 w-4" /> Mark all as read
    </Button>
  </Card.Footer>
</Card.Root>
