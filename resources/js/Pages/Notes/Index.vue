<script setup>
import AppLayout from '@/Layouts/AppLayout.vue';
import { Link } from '@inertiajs/inertia-vue3';
import { ref } from 'vue';
import { Inertia } from '@inertiajs/inertia'

defineProps({
    notes: Array
});

const valor = ref(null);

const destroy = (noteId) => {
    if (confirm('¿Desea eliminar la nota?')) {
        Inertia.delete(route('notes.destroy', noteId));
    }
}

const search = () => {
    let q = valor.value;
    Inertia.get(route('notes.index', {q}), {}, { preserveState: true });
};
</script>

<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Módulo de Notas
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="md:grid md:grid-cols-3 md:gap-6">

                    <div class="md:col-span-1">
                        <div class="px-4 sm:px0">
                            <h3 class="text-lg text-gray-900">Listado de Notas</h3>
                            <p class="text-sm text-gray-600">
                                Toma el registro correcto y ejecuta cualquier función (ver, editar o eliminar)
                            </p>
                        </div>
                    </div>

                    <div class="md:col-span-2 mt-5 md:mt-0">
                        <div class="shadow bg-white md:rounded-md p-4">
                            <div class="flex justify-between">
                                <input type="text" class="form-input rounded-md shadow-sm" placeholder="Buscar..." v-model="valor" @keyup="search">
                                <Link
                                    :href="route('notes.create')"
                                    class="bg-emerald-500 text-white font-bold px-4 py-2 rounded-md"
                                >
                                    Crear
                                </Link>
                            </div>
                            <hr class="my-4">
                            <table>
                                <tr v-for="note in notes" v-bind:key="note.id">
                                    <td class="border px-4 py-2">
                                        {{ note.excerpt }}
                                    </td>
                                    <td class="border px-1 py-2">
                                        <Link
                                            :href="route('notes.show', note)"
                                            class="bg-blue-500 hover:bg-blue-600 text-white rounded-sm font-bold py-1 px-2"
                                        >
                                            Ver
                                        </Link>
                                    </td>
                                    <td class="border px-1 py-2">
                                        <Link
                                            :href="route('notes.edit', note)"
                                            class="bg-emerald-500 hover:bg-emerald-600 text-white rounded-sm font-bold py-1 px-2"
                                        >
                                            Editar
                                        </Link>
                                    </td>
                                    <td class="border px-1 py-2">
                                        <a
                                            href="#" @click.prevent="destroy(note.id)"
                                            class="bg-rose-500 hover:bg-rose-600 text-white rounded-sm font-bold py-1 px-2"
                                        >
                                            Eliminar
                                        </a>
                                    </td>
                                </tr>
                            </table>
                        </div>
                    </div>

                </div>
            </div>
        </div>
    </AppLayout>
</template>
