<template>
    <div :class="['doc-component', className]">
        <Head>
            <Title>Volt | {{ title }}</Title>
            <Meta name="description" :content="'Volt | ' + description" />
        </Head>

        <ul class="doc-tabmenu">
            <li :class="{ 'doc-tabmenu-active': tab === 0 }">
                <button type="button" @click="tab = 0">FEATURES</button>
            </li>
            <li v-if="isComponent" :class="{ 'doc-tabmenu-active': tab === 1 }">
                <button type="button" @click="tab = 1">CODE</button>
            </li>
        </ul>

        <div class="doc-tabpanels">
            <div v-show="tab === 0" class="doc-tabpanel">
                <div class="doc-main">
                    <div class="doc-intro">
                        <h1>{{ header }}</h1>
                        <p>
                            <span>{{ description }}</span>
                        </p>
                        <div v-if="isComponent" class="pt-3 flex gap-2">
                            <a
                                :href="`https://primevue.org${originPath}/#api`"
                                target="_blank"
                                rel="noopener noreferrer"
                                class="inline-flex rounded-full px-3 py-1 bg-surface-200 hover:bg-surface-300 transition-all duration-200 gap-2 items-center text-sm dark:bg-surface-800 dark:hover:bg-surface-700"
                                ><span class="text-surface-900 dark:text-surface-50 font-medium">API</span><i class="pi pi-external-link text-xs! text-surface-900 dark:text-surface-50"></i
                            ></a>
                            <a
                                :href="`https://primevue.org${originPath}/#pt`"
                                target="_blank"
                                rel="noopener noreferrer"
                                class="inline-flex rounded-full px-3 py-1 bg-surface-200 hover:bg-surface-300 transition-all duration-200 gap-2 items-center text-sm text-surface-900 dark:bg-surface-800 dark:hover:bg-surface-700"
                                ><span class="text-surface-900 dark:text-surface-50 font-medium">PassThrough</span><i class="pi pi-external-link text-xs! text-surface-900 dark:text-surface-50"></i
                            ></a>
                            <a
                                :href="`https://primevue.org${originPath}/#accessibility`"
                                target="_blank"
                                rel="noopener noreferrer"
                                class="inline-flex rounded-full px-3 py-1 bg-surface-200 hover:bg-surface-300 transition-all duration-200 gap-2 items-center text-sm text-surface-900 dark:bg-surface-800 dark:hover:bg-surface-700"
                                ><span class="text-surface-900 dark:text-surface-50 font-medium">Accessibility</span><i class="pi pi-external-link text-xs! text-surface-900 dark:text-surface-50"></i
                            ></a>
                        </div>
                    </div>
                    <DocSections :docs="componentDocs" />
                </div>
                <DocSectionNav :docs="componentDocs" />
            </div>

            <template v-if="tab === 1">
                <div class="doc-tabpanel">
                    <DocPreset :presetKey="header" :introText="`${header} Code`" />
                </div>
                <template v-if="presetKeys.length > 0">
                    <div v-for="(cmp, index) in presetKeys" :key="index" class="doc-tabpanel">
                        <DocPreset :presetKey="cmp" :introText="`${cmp} Code`" />
                    </div>
                </template>
            </template>
        </div>
    </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue';

defineProps({
    title: String,
    header: String,
    description: String,
    componentDocs: Object,
    className: String,
    presetDoc: Object,
    isComponent: {
        type: Boolean,
        default: true
    },
    presetKeys: {
        type: Array as () => string[],
        default: () => []
    }
});

const route = useRoute();
const tab = ref(0);

const originPath = computed(() => route.path);
</script>
