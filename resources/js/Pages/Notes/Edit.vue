<script setup>
import AppLayout from '@/Layouts/AppLayout.vue';
import { useForm , Link } from '@inertiajs/inertia-vue3';

const props = defineProps({
    note: Object,
});

const form = useForm({
    excerpt: props.note.excerpt,
    content: props.note.content
});

const submit = () => {
    form.put(route('notes.update', props.note), form);
}
const destroy = () => {
    if (confirm('¿Desea eliminar la nota?')) {
        form.delete(route('notes.destroy', props.note));
    }
}
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
                            <h3 class="text-lg text-gray-900">Editar una nota</h3>
                            <p class="text-sm text-gray-600">
                                Si editas no podrás volver al estado anterior
                            </p>
                        </div>
                    </div>

                    <div class="md:col-span-2 mt-5 md:mt-0">
                        <div class="shadow bg-white md:rounded-md p-4">
                            <form @submit.prevent="submit">
                                <label class="block font-medium text-sm text-gray-700">
                                    Resumen
                                </label>
                                <textarea
                                    class="form-input w-full rounded-md shadow-sm"
                                    v-model="form.excerpt"
                                ></textarea>
                                <label class="block font-medium text-sm text-gray-700">
                                    Contenido
                                </label>
                                <textarea
                                    class="form-input w-full rounded-md shadow-sm"
                                    v-model="form.content"
                                    rows="8"
                                ></textarea>
                                <button
                                    class="bg-emerald-500 hover:bg-emelard-600 text-white rounded-sm font-bold py-2 px-4 mr-2"
                                >Editar</button>
                                <a
                                    href="#" @click.prevent="destroy"
                                    class="bg-rose-500 hover:bg-rose-600 text-white rounded-sm font-bold py-2 px-4 mr-2"
                                >Eliminar nota</a>
                                <Link
                                    :href="route('notes.index')"
                                    class="bg-blue-500 hover:bg-blue-600 text-white rounded-sm font-bold py-2 px-4"
                                >Volver</Link>
                            </form>
                        </div>
                    </div>

                </div>
            </div>
        </div>
    </AppLayout>
</template>
