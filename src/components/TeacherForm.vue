<template>
    <section>
        <h3>Añadir Profesor</h3>
        <div><label>Nombres:</label><input type="text" v-model="teacher.teacherName"></div>
        <div><label>Apellidos:</label><input type="text" v-model="teacher.surname"></div>
        <div><label>DNI:</label><input type="text" v-model="teacher.dni"></div>
        <div><label>Materias:</label><input type="text" v-model="subject"><button @click="handlesubject">Agregar</button></div>
        <div>
            <ul>
                <li v-for="(elm, index) in teacher.subjects" :key="index">{{ elm }}</li>
            </ul>
        </div>
        <input type="checkbox" v-model="teacher.doc"/>Documentacion Entregada
        <button @click="handleTeacher()">Agregar</button>
    </section>

    <section>
        <h3>Listado de profesores</h3>
        <table>
            <tr>
                <th>Nombres</th>
                <th>Apellidos</th>
                <th>DNI</th>
                <th>Materias</th>
                <th>Documentacion Entregada</th>
            </tr>
            <tr v-for="elm in teachers" :key="elm.dni">
                <th>{{ elm.teacherName }}</th>
                <th>{{ elm.surname }}</th>
                <th>{{ elm.dni }}</th>
                <th>
                    <ul>
                        <li v-for="(item, index) in elm.subjects" :key="index">{{ item }}</li>
                    </ul>
                </th>
                <th v-if="elm.doc">Entregada</th>
                <th v-else>No Entregada</th>
            </tr>
        </table>
    </section>
</template>

<script lang="ts" setup>
    import {Ref, ref} from 'vue'

    interface ITeacher {
        teacherName: string,
        surname: string,
        dni: number,
        subjects: Array<string>,
        doc: boolean
    }

    let teacher:Ref = ref({
        teacherName: '',
        surname: '',
        dni: '',
        subjects: [],
        doc: false
    })

    let teachers:Ref<Array<ITeacher>> = ref([])

    let subject:Ref<string> = ref('')

    const handlesubject = () => {
        teacher.value.subjects.push(subject.value)
        subject.value = ""
    }

    const handleTeacher = () => {
        teachers.value.push({
            teacherName: teacher.value.teacherName,
            surname: teacher.value.surname,
            dni: teacher.value.dni,
            subjects: teacher.value.subjects,
            doc: teacher.value.doc
        })
        teacher.value.teacherName = ""
        teacher.value.surname = ""
        teacher.value.dni = ""
        teacher.value.subjects = []
        teacher.value.doc = false
    }

</script>

<style scoped>
</style>