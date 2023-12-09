<template>
  <header class="sticky top-0 z-30 border-b bg-background/80 backdrop-blur">
    <div class="container flex h-14 items-center justify-between">
      <div class="flex items-center gap-10">
        <div class="flex items-center gap-5">
          <UiButton
            @click="mobileNav = true"
            size="icon-sm"
            variant="outline"
            class="h-9 w-9 lg:hidden"
            ><Icon name="heroicons:bars-2" class="h-4 w-4" />
          </UiButton>
          <NuxtLink to="/" class="text-lg font-bold">Nuxt Starter</NuxtLink>
        </div>
        <nav class="hidden items-center space-x-6 text-sm font-medium lg:flex">
          <NuxtLink
            :class="[$route.path == '/' ? '!text-primary' : '']"
            to="/"
            class="text-foreground/60 transition-colors hover:text-foreground"
            >Home</NuxtLink
          >
          <NuxtLink
            :class="[
              $route.path.includes('about') || $route.path.includes('/forms/')
                ? '!text-primary'
                : '',
            ]"
            to="/about"
            class="text-foreground/60 transition-colors hover:text-foreground"
            >About</NuxtLink
          >
          <UiDropdownMenu>
            <UiDropdownMenuTrigger>
              <div
                class="inline-flex items-center gap-1 text-foreground/60 transition-colors hover:text-foreground"
              >
                <span>Dropdown</span>
                <Icon name="heroicons:chevron-down" class="h-3 w-3" />
              </div>
            </UiDropdownMenuTrigger>
            <UiDropdownMenuContent align="start" :side-offset="5">
              <UiDropdownMenuItem as-child>
                <NuxtLink class="cursor-pointer hover:bg-muted" to="/about"
                  >about</NuxtLink
                >
              </UiDropdownMenuItem>
              <UiDropdownMenuItem as-child>
                <NuxtLink class="cursor-pointer hover:bg-muted" to="/about"
                  >about2</NuxtLink
                >
              </UiDropdownMenuItem>
            </UiDropdownMenuContent>
          </UiDropdownMenu>
        </nav>
      </div>

      <div class="flex items-center">
        <UiButton
          to="https://github.com/mciluke"
          target="_blank"
          class="h-9 w-9"
          variant="ghost"
          size="icon"
          ><Icon name="radix-icons:github-logo" class="h-[18px] w-[18px]"
        /></UiButton>
        <UiDropdownMenu>
          <UiDropdownMenuTrigger as-child>
            <UiButton class="h-9 w-9" variant="ghost" size="icon"
              ><Icon :name="currentIcon || 'lucide:sun'" class="h-[18px] w-[18px]"
            /></UiButton>
          </UiDropdownMenuTrigger>
          <UiDropdownMenuContent align="end" :side-offset="5">
            <UiDropdownMenuItem
              class="cursor-pointer"
              v-for="(m, i) in modes"
              :key="i"
              :icon="m.icon"
              :title="m.title"
              @click="setTheme(m.value)"
            />
          </UiDropdownMenuContent>
        </UiDropdownMenu>
      </div>
    </div>
    <MobileNav v-model="mobileNav" />
  </header>
</template>

<script lang="ts" setup>
  const modes = [
    { icon: "lucide:sun", title: "Light", value: "light" },
    { icon: "lucide:moon", title: "Dark", value: "dark" },
    { icon: "lucide:laptop", title: "System", value: "system" },
  ];

  const mobileNav = ref(false);

  const colorMode = useColorMode();
  const setTheme = (val: string) => {
    colorMode.preference = val;
  };

  const currentIcon = computed(() => {
    return modes.find((m) => m.value === colorMode?.preference)?.icon;
  });

  const isOpen = ref(false);

  // const { metaSymbol } = useShortcuts();

  // defineShortcuts({
  //   meta_k: () => {
  //     isOpen.value = !isOpen.value;
  //   },
  // });
</script>