<template>
    <Page>
        <ActionBar>
            <Label text="Converter"/>
        </ActionBar>

        <GridLayout rows="*, *" columns="*">
            <Button v-for="page in pages" :key="page.id" :row="page.id" :text="page.name" @tap="Go(page.id)" />
        </GridLayout>
    </Page>
</template>

<script>
import Time from './Time.vue';
import Weight from './Weight.vue';
    export default {
        data () {
            return {
                pages: [
                    {id: 0, name: 'ToTime', value: Time},
                    {id: 1, name: 'ToWeight', value: Weight},
                ]
            };
        },
        methods: {
            Go: function(id) {
                this.$navigateTo(this.pages[id].value);
            }
        }
    };
</script>

<style scoped lang="scss">
    @import '@nativescript/theme/scss/variables/blue';
    @import 'app/app.scss';
</style>
