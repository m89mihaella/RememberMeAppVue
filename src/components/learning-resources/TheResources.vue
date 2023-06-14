<template>
  <base-card>
    <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">Stored Resources</base-button>
    <base-button @click="setSelectedTab('add-resource')" :mode="addResButtonMode">Add Resource</base-button></base-card
  >
 <keep-alive><component :is="selectedTab"></component></keep-alive> 
</template>

<script>
import StoredResources from "./StoredResources.vue";
import AddResource from "./AddResource.vue";
export default {
  components: { StoredResources, AddResource },
  data() {
    return {
      selectedTab: "stored-resources",
      storedResources: [
        {
          id: "nuxt",
          title: "Mastering Nuxt",
          description: "Learn how to build a real world Nuxt app",
          link: "https://masteringnuxt.com",
        },
        {
          id: "nuxt-docs",
          title: "Nuxt.js docs",
          description: "The place to learn about Nuxt and start contributing",
          link: "https://nuxtjs.org",
        },
        {
          id: "vue",
          title: "Vue.js docs",
          description: "The place to learn about Vue and start contributing",
          link: "https://vuejs.org",
        },
      ],
    };
  },
  provide() {
    return {
        resources: this.storedResources,
        addResource: this.addResource,
      deleteResource:this.deleteResource,
    };
  },
    computed: {
        storedResButtonMode() {
            return this.selectedTab === 'stored-resources' ? null : 'flat';
        },
        addResButtonMode() {
            return this.selectedTab === 'add-resource' ? null : 'flat';
        }
    },

  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
      },
      addResource(title, description, url) {
          const newResource = {
                id: new Date().toISOString(),
                title:title,
                description:description,
                link: url
          };
          this.storedResources.unshift(newResource);
            this.setSelectedTab('stored-resources');
      },
      deleteResource(resId) {
          const resIndex = this.storedResources.findIndex(res => res.id === resId);
            this.storedResources.splice(resIndex, 1);
        }
    },

    
  }
</script>
