<template>
    <div v-bind:class="[
        { [$style.visibleContainer] : hasExpandedMenu },
        $style.container
        ]"
    >
        <header v-bind:class="$style.headerTop">
            <nav
                v-bind:class="$style.primaryNavigation"
            >
                <ul>
                    <li
                        v-for="(item, index) in nav.items"
                        v-bind:key="index"
                        v-on:click="closeMenu"
                        v-bind:class="$style.navItem"
                    >
                        <nuxt-link
                            v-bind:class="$style.navLink"
                            v-bind:to="item.link">{{ item.name }}
                        </nuxt-link>
                    </li>
                </ul>
            </nav>
        </header>
        <div v-bind:class="[
            { [$style.headerBottomShift] : hasExpandedMenu },
            $style.headerBottom
            ]"
        >
            <AppImage
                image="static/images/jnh-logo.png"
                alt="Jeff Horner logo"
                v-bind:class="$style.logo"
            >
            </AppImage>
            <button
                v-on:click="toggleMenu"
                v-bind:class="$style.menuBarsBtn"
            >
                <AppIcon
                    v-bind:name="hasExpandedMenu ? 'times' : 'bars'"
                />
            </button>
        </div>
    </div>
</template>

<script>
    import AppImage from '@/components/framework/AppImage';
    import AppIcon from '@/components/framework/AppIcon';

    export default {
        components: {
            AppImage,
            AppIcon,
        },
        data () {
            return {
                hasExpandedMenu: false,
                nav: {
                    items: [
                        {
                            name: 'home',
                            link: '/',
                        },
                        {
                            name: 'portfolio',
                            link: '/portfolio',
                        },
                        {
                            name: 'about',
                            link: 'about',
                        },
                        {
                            name: 'learn-to-code',
                            link: '/learn-to-code',
                        },
                        {
                            name: 'blog',
                            link: '/blog',
                        },
                        {
                            name: 'contact',
                            link: '/contact',
                        },
                    ],
                },
            };
        },
        methods: {
            toggleMenu () {
                this.hasExpandedMenu = !this.hasExpandedMenu;
            },
            closeMenu () {
                if (this.hasExpandedMenu) {
                    console.log('test');
                    this.hasExpandedMenu = false;
                }
            }
        },
    }
</script>

<style lang="scss" module>

    .container {
        @apply items-center flex flex-col;
        transition: transform 500ms;
        transform: translateY(-75%);

        &.visibleContainer {
            transform: translateY(0);
        }
    }

    .headerTop {
        @apply flex flex-row-reverse w-full;
    }

    .headerBottom {
        @apply flex flex-row justify-between mt-8 mx-10 w-full;
        max-width: 75%;
    }

    .primaryNavigation {
        @apply w-full;

        ul {
            @apply flex flex-row text-center pl-0;
            height: 100%;
        }

        .navItem {
            @apply list-reset w-1/5;
            background-color: #F3F3F3;
            border: 1px solid #DDDDDD;
            transition: all .2s ease-in-out;

            &:hover {
                border-color: #0071FF;
                background-color: #0071FF;

                > a {
                    color: #fff;
                }
            }

            .navLink {
                @apply block font-semibold h-full no-underline text-sm;
                color: #262626;
                padding: 6.5rem 0;
            }
        }
    }

    .menuBarsBtn {
        @apply z-50;

        &:focus {
            @apply outline-none;
        }
    }

    .logo {
        @apply h-12 w-12;

        > img {
            @apply h-full w-full;
        }
    }

</style>
