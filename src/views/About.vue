<template>
    <div>
        <div
            v-if="pokemon"
            class="w-3/12 m-auto bg-purple-100 mt-4 p-4 shadow-2xl flex justify-center flex-col items-center"
        >
            <h3 class="text-2xl text-green-900 uppercase">
                {{ pokemon.name }}
            </h3>
            <div class="flex justify-center">
                <img :src="pokemon.sprites.front_default" alt="" />
                <img :src="pokemon.sprites.back_default" alt="" />
            </div>
            <h3 class="text-yellow-400">Type</h3>
            <div class="flex mt-4">
                <div v-for="(type, idx) in pokemon.types" :key="idx">
                    <h5
                        class="text-blue-900 uppercase px-2 rounded bg-blue-50 mr-2"
                    >
                        {{ type.type.name }}
                    </h5>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { useRoute } from 'vue-router'
import { reactive, toRefs } from 'vue'
export default {
    setup() {
        const route = useRoute()
        const state = reactive({
            pokemon: null,
        })
        fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}`)
            .then(res => res.json())
            .then(data => {
                // console.log(data)
                state.pokemon = data
            })
        return { ...toRefs(state) }
    },
}
</script>
