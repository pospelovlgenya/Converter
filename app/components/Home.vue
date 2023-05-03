<template>
    <Page>
        <ActionBar>
            <Label text="Converter"/>
        </ActionBar>

        <GridLayout rows="auto, auto, auto, auto, auto" columns="*">
            <Button v-for="page in pages" :key="page.id" :row="page.id" :text="page.name" @tap="Go(page.id)" />
        </GridLayout>
    </Page>
</template>

<script>
import Time from './Time.vue';
import Weight from './Weight.vue';
import Volume from './Volume.vue';
import Temperature from './Temperature.vue';
import Data from './Data.vue';

    export default {
        data () {
            return {
                pages: [
                    {id: 0, name: 'Данные', value: Data},
                    {id: 1, name: 'Температура', value: Temperature},
                    {id: 2, name: 'Время', value: Time},
                    {id: 3, name: 'Объём', value: Volume},
                    {id: 4, name: 'Вес', value: Weight},
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
