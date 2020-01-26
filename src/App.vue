<template>
    <v-app id="inspire">
        <v-navigation-drawer v-model="drawer" app>
            <v-list dense>
                <v-list-item to="/">
                    <v-list-item-action>
                        <v-icon>fas fa-table</v-icon>
                    </v-list-item-action>
                    <v-list-item-content>
                        <v-list-item-title>Home</v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
                <v-list-item to="/about">
                    <v-list-item-action>
                        <v-icon>mdi-contact-mail</v-icon>
                    </v-list-item-action>
                    <v-list-item-content>
                        <v-list-item-title>About</v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
            </v-list>
        </v-navigation-drawer>

        <v-app-bar app color="indigo" dark>
            <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
            <v-toolbar-title>Test-KT</v-toolbar-title>
        </v-app-bar>

        <v-content>
            <v-container>
                <v-row justify="center">
                    <v-col class="text-center">
                        <router-view></router-view>
                    </v-col>
                </v-row>
            </v-container>
        </v-content>

        <v-footer app color="indigo">
            <span class="white--text">&copy; 2020</span>
        </v-footer>
    </v-app>
</template>

<script>
export default {
    data: () => ({
        drawer: null
    })
};
</script>
