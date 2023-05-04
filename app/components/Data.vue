<template>
    <Page>
        <ActionBar>
            <NavigationButton text="Домой" android.systemIcon="ic_menu_back" @tap="GoToHome()" />
            <Label text="Данные"/>
        </ActionBar>

        <FlexboxLayout flexDirection="column">
            <FlexboxLayout flexDirection="column">
                <Label text="Величина для конвертации:"/>
                <TextField v-model="inputValue" keyboardType="number"/>
                <ListPicker :items="getValues()" v-model="selectedValue"/>
            </FlexboxLayout>
            <FlexboxLayout>

            </FlexboxLayout>
        </FlexboxLayout>
    </Page>
</template>

<script>
import Home from './Home.vue';
    export default {
        data () {
            return {
                inputValue: 0,
                selectedValue: 0,
                values: [
                    {name: 'бит', coef: 1, forInput: 0},
                    {name: 'Байт', coef: 8, forInput: 0},
                    {name: 'КБ', coef: 8*10**3, forInput: 0},
                    {name: 'МБ', coef: 8*10**6, forInput: 0},
                    {name: 'ГБ', coef: 8*10**9, forInput: 0},
                    {name: 'ТБ', coef: 8*10**12, forInput: 0},
                    {name: 'ПБ', coef: 8*10**15, forInput: 0}
                ]
            };
        },
        methods: {
            GoToHome: function() {
                this.$navigateTo(Home);
            },
            getValues: function() {
                let comp = [];
                for (i = 0; i < this.values.length; i++) {
                    comp.push(this.values[i].name);
                }
                return comp;
            }
        }
    };
</script>

<style scoped lang="scss">
    @import '@nativescript/theme/scss/variables/blue';
    @import 'app/app.scss';
</style>