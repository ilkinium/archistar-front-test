<template>
    <div class="sidebar-filters">
        <a-menu mode="inline" theme="dark"
                v-model="selectedCategory"
        >
            <a-sub-menu key="category">
                <span slot="title"><a-icon type="bars"/><span>Category</span></span>
                <a-menu-item v-for="(category, index) in categories"
                             :key="index"
                             @click="handleFilter('select-category', category, 'selectedCategory', 'categories', index)"
                >
                    {{ category }}
                </a-menu-item>
            </a-sub-menu>
        </a-menu>

        <a-menu mode="inline" theme="dark"
                v-model="selectedStatus"
        >
            <a-sub-menu key="status">
                <span slot="title"><a-icon type="filter"/><span>Status</span></span>
                <a-menu-item v-for="(status, index) in statuses"
                             :key="`status${index}`"
                             @click="handleFilter('select-status', status, 'selectedStatus', 'statuses', index)"
                >
                    {{ status }}
                </a-menu-item>
            </a-sub-menu>
        </a-menu>
    </div>
</template>

<script>
    export default {
        name: "SideBar",
        props: {
            blob: Object
        },

        data() {
            return {
                categories: [],
                statuses: [],
                selectedCategory: [],
                selectedStatus: [],
            }
        },

        mounted() {
            this.categories = this.setFilterByName('Category');
            this.statuses = this.setFilterByName('Status');
        },

        methods: {
            setFilterByName(name) {
                return Array.from(new Set(this.blob.features.map(item => item.properties.project[name])))
            },

            handleFilter(emitName, value, selectedKey, sourceArray, index) {
                if (this[sourceArray][index] === value) {
                    this[selectedKey] = [];
                }
                this.$nextTick(() => {
                    this.$emit(emitName, this[selectedKey].length === 0 ? '' : value);
                })
            }
        }
    }
</script>

<style scoped>

</style>