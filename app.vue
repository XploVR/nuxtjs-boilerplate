<!-- src/App.vue -->
<template>
  <TooltipProvider>
    <AuthProvider>
      <CartProvider>
        <div class="min-h-screen w-full flex overflow-x-hidden bg-background">
          <!-- Sidebar -->
          <aside
            class="shrink-0 border-r border-sidebar-border bg-sidebar text-sidebar-foreground transition-[width] duration-200"
            :class="isSidebarOpen ? 'w-0' : 'w-16'"
          >
            <!-- … your sidebar content … -->
          </aside>

          <!-- Main column -->
          <div class="flex-1 flex flex-col min-w-0">
            <!-- Header -->
            <header
              class="h-14 sm:h-16 border-b border-border bg-background
                     flex items-center justify-between px-3 sm:px-4
                     relative z-50"
            >
              <!-- mobile sidebar toggle -->
              <button
                class="p-2 hover:bg-muted rounded-md min-h-touch min-w-touch sm:hidden"
                aria-label="Toggle sidebar"
                @click="isSidebarOpen = !isSidebarOpen"
              >
                <Menu class="h-5 w-5" />
              </button>

              <!-- titles -->
              <h1 class="text-sm font-medium text-foreground hidden sm:block">
                <span class="font-typografix">xplor</span> Workspace
              </h1>
              <h1 class="text-mobile-sm font-medium text-foreground sm:hidden">
                <span class="font-typografix">xplor</span>
              </h1>
            </header>

            <!-- Routed pages -->
            <main class="flex-1 min-w-0">
              <RouterView />
            </main>
          </div>
        </div>

        <!-- UI singletons (once, at app root) -->
        <Toaster />
        <!-- Remove <Sonner /> if Toaster already wraps vue-sonner -->
      </CartProvider>
    </AuthProvider>
  </TooltipProvider>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { RouterView } from 'vue-router'

// Providers / singletons
import TooltipProvider from '@/components/ui/tooltip/TooltipProvider.vue'
import Toaster from '@/components/ui/toaster/Toaster.vue'
// import Sonner from '@/components/ui/sonner/Sonner.vue' // usually not needed if Toaster uses vue-sonner
import AuthProvider from '@/components/AuthProvider.vue'
import CartProvider from '@/components/CartProvider.vue'

// Icons / controls
import { Menu } from 'lucide-vue-next'
// If you actually have a SidebarTrigger component, import & use it instead of the <button>:
// import SidebarTrigger from '@/components/SidebarTrigger.vue'

const isSidebarOpen = ref(true)

onMounted(() => {
  console.log('[App] mounted')
})
</script>




