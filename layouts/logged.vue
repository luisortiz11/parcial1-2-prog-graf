<template>
  <a-layout id="components-layout-demo-custom-trigger">
    <a-layout-sider theme='light' v-model="collapsed" :trigger="null" collapsible>
      <a-icon
      class="trigger"
      :type="collapsed ? 'menu-unfold' : 'menu-fold'"
      @click="() => (collapsed = !collapsed)"
      />
      
      <a-menu theme="light" mode="inline" :default-selected-keys="['1']">
        <a-menu-item key="1">
          <a-icon type="home" />
          <span>Inicio</span>
        </a-menu-item>
        <a-menu-item key="2">
          <a-icon type="folder-open" />
          <span>Expedientes </span>
        </a-menu-item>
        <a-divider/>
        <a-menu-item key="3">
          <a-icon type="file-text" />
          <span>Reportes</span>
        </a-menu-item>
        <a-divider/>
        <a-menu-item key="4">
          <a-icon type="setting" />
          <span>Configuración</span>
        </a-menu-item>
        <a-menu-item key="5">
          <a-icon type="car" />
          <span>Aseguradora</span>
        </a-menu-item>
        <a-menu-item key="6">
          <a-icon type="user" />
          <span>Usuarios</span>
        </a-menu-item>
        <a-menu-item key="7">
          <a-icon type="bank" />
          <span>Juzgado</span>
        </a-menu-item>
      </a-menu>
    </a-layout-sider>
    <a-layout>
    <a-layout-header class="header" :style="{ background: 'white'}">
      
      <h1>NOMBRE</h1>
    </a-layout-header>
      <a-layout-content
        :style="{ padding: '10px', background: 'white', minHeight: '660px' }"
      >
        <Nuxt/>
      </a-layout-content>
    </a-layout>
  </a-layout>
</template>
<script>
export default {
  data() {
    return {
      collapsed: false,
    };
  },
};
</script>
<style>
#components-layout-demo-custom-trigger .trigger {
  font-size: 18px;
  line-height: 64px;
  padding: 0 24px;
  cursor: pointer;
  transition: color 0.3s;
}

#components-layout-demo-custom-trigger .trigger:hover {
  color: #cecece;
}

#components-layout-demo-custom-trigger{
  background: #cecece;
}


</style>
