<template>
    <Page>
        <ActionBar>
            <Label text="Данные"/>
        </ActionBar>

        <GridLayout rows="auto" columns="*">
            <Button text="Домой" @tap="GoToHome()" />
        </GridLayout>
    </Page>
</template>

<script>
import Home from './Home.vue';
    export default {
        data () {
            return {
            };
        },
        methods: {
            GoToHome: function() {
                this.$navigateTo(Home);
            }
        }
    };
</script>

<style scoped lang="scss">
    @import '@nativescript/theme/scss/variables/blue';
    @import 'app/app.scss';
</style>