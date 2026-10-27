<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="app-header">
      <q-toolbar class="q-px-md">
        <q-btn flat dense round icon="menu" aria-label="Menu" @click="toggleLeftDrawer" />

        <q-toolbar-title class="row items-center no-wrap font-display text-weight-bold">
          <q-icon name="qr_code_2" size="22px" class="q-mr-sm text-primary" />
          {{ $q.screen.gt.xs ? 'Quasar QRCode Reader' : 'QR Reader' }}
        </q-toolbar-title>

        <q-btn
          flat
          round
          dense
          icon="code"
          aria-label="GitHub"
          type="a"
          href="https://github.com/patrickmonteiro/quasar-qrcode-reader"
          target="_blank"
        >
          <q-tooltip>Ver no GitHub</q-tooltip>
        </q-btn>
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above :width="232" class="app-drawer" dark>
      <div class="app-drawer__brand">
        <q-icon name="qr_code_2" size="22px" class="text-primary" />
        <span class="text-weight-bold font-display">QR Reader</span>
      </div>

      <q-list padding class="app-drawer__list">
        <q-item-label header class="app-drawer__section-label">Ferramentas</q-item-label>

        <q-item
          v-for="item in toolItems"
          :key="item.to"
          clickable
          dense
          :to="item.to"
          exact
          class="app-drawer__item"
          active-class="app-drawer__item--active"
          @click="closeOnMobile"
        >
          <q-item-section avatar class="app-drawer__item-icon">
            <q-icon :name="item.icon" size="18px" />
          </q-item-section>
          <q-item-section class="text-body2">{{ item.label }}</q-item-section>
        </q-item>

        <q-item-label header class="app-drawer__section-label">Links</q-item-label>

        <q-item
          v-for="item in linkItems"
          :key="item.href"
          clickable
          dense
          tag="a"
          target="_blank"
          :href="item.href"
          class="app-drawer__item"
        >
          <q-item-section avatar class="app-drawer__item-icon">
            <q-icon :name="item.icon" size="18px" />
          </q-item-section>
          <q-item-section class="text-body2">{{ item.label }}</q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>

    <q-footer class="app-footer">
      Desenvolvido por
      <a href="https://pulsarcode.com.br" target="_blank" rel="noopener noreferrer">Pulsar Code</a>
      <span class="app-footer__sep">·</span>
      <a
        href="https://github.com/patrickmonteiro/quasar-qrcode-reader"
        target="_blank"
        rel="noopener noreferrer"
        class="app-footer__repo"
      >
        <!-- GitHub mark (Octicons, MIT) — Material Symbols has no brand icons -->
        <svg viewBox="0 0 16 16" width="12" height="12" aria-hidden="true">
          <path
            fill="currentColor"
            d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"
          />
        </svg>
        Star on GitHub
      </a>
    </q-footer>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'
import { useQuasar } from 'quasar'

const $q = useQuasar()

const leftDrawerOpen = ref($q.screen.gt.sm)

const toolItems = [
  { to: '/', icon: 'camera_alt', label: 'Read QRCode' },
  { to: '/generator', icon: 'select_all', label: 'QRCode Generator' },
]

const linkItems = [
  { href: 'https://quasar.dev', icon: 'school', label: 'Docs Quasar' },
  { href: 'https://pulsarcode.com.br', icon: 'open_in_new', label: 'pulsarcode.com.br' },
]

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value
}

function closeOnMobile() {
  if ($q.screen.lt.md) leftDrawerOpen.value = false
}
</script>

<style scoped>
.app-header {
  background: var(--pulsar-sidebar-bg);
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
}

.app-drawer {
  background: var(--pulsar-sidebar-bg);
}

.app-drawer__brand {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 18px 16px;
  color: #fff;
  font-size: 15px;
}

.app-drawer__section-label {
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  color: #71717a;
  padding: 16px 16px 6px;
  min-height: 0;
}

.app-drawer__item {
  border-radius: 8px;
  margin: 1px 8px;
  min-height: 36px;
  color: #d4d4d8;
}

.app-drawer__item--active {
  color: #fff;
  background: rgba(16, 185, 129, 0.16);
}

.app-drawer__item--active .q-icon {
  color: var(--q-primary);
}

.app-drawer__item-icon {
  min-width: 28px;
}

.app-drawer__list {
  padding-bottom: 24px;
}

.app-footer {
  background: var(--pulsar-sidebar-bg);
  border-top: 1px solid rgba(255, 255, 255, 0.08);
  padding: 8px 16px;
  font-size: 11px;
  text-align: center;
  color: #a1a1aa;
}

.app-footer a {
  color: var(--q-primary);
  font-weight: 600;
  text-decoration: none;
}

.app-footer a:hover {
  text-decoration: underline;
}

.app-footer__sep {
  margin: 0 6px;
  opacity: 0.6;
}

.app-footer__repo {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  vertical-align: middle;
}
</style>
