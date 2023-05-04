<template>
    <Page class="page">
        <ActionBar class="ab">
            <NavigationButton android.systemIcon="ic_menu_back" @tap="GoToHome()" class="header" />
            <Label text="Температура" class="header"/>
        </ActionBar>

        <FlexboxLayout flexDirection="column">
            <FlexboxLayout flexDirection="column">
                <Label text="Величина для конвертации:" class="text"/>
                <TextField v-model="inputValue" keyboardType="number" class="text"/>
                <ListPicker :items="getValues()" v-model="selectedValue" class="text"/>
            </FlexboxLayout>
            <FlexboxLayout flexDirection="column">
                <Label text="Это равняется:" class="text"/>
                <Label v-for="value in values" :key="value.name" class="text">{{ value.forInput }} {{ value.name }}</Label>
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
                    {name: 'Градусы Цельсия',  forInput: 0},
                    {name: 'Градусы Фаренгейта',  forInput: 0},
                    {name: 'Градусы Кельвина',  forInput: 0},
                ],
            };
        },
        watch: {
            inputValue: function() {
                this.getResult();
            },
            selectedValue: function() {
                this.getResult();
            },
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
            },
            getResult: function() {
                let input = Number(this.inputValue);
                switch(this.selectedValue) {
                    case 0: // Цельс
                        this.values[0].forInput = input;
                        this.values[1].forInput = input * 1.8 + 32;
                        this.values[2].forInput = input + 273.15;
                    break;
                    case 1: // Фарен
                        this.values[0].forInput = (input - 32)*0.5555555555556;
                        this.values[1].forInput = input;
                        this.values[2].forInput = this.values[0].forInput + 273.15
                    break;
                    case 2: // Кельв
                        this.values[0].forInput = input - 273.15;
                        this.values[1].forInput = (input - 273.15) * 1.8 + 32;
                        this.values[2].forInput = input;
                    break;
                }
            }
        },
    };
</script>

<style scoped lang="scss">
    @import '@nativescript/theme/scss/variables/blue';
    @import 'app/app.scss';
</style>