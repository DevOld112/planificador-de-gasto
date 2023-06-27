<script setup>
import { computed } from 'vue'
import "vue3-circle-progress/dist/circle-progress.css";
import CircleProgress from "vue3-circle-progress";
import { formatearCantidad } from '../helper'

defineEmits(['reset-app'])


const props = defineProps({
    presupuesto: {
        type: Number,
        required: true
    },
    disponible: {
        type: Number,
        required: true
    },
    gastado: {
    type: Number,
    required: true,
    },
    inventado: {
        type: Number,
        required: true
    }
})

const porcentaje = computed(() =>{
   return parseInt(((props.presupuesto - props.disponible) / props.presupuesto) * 100)
})

</script>

<template>
    <div class="dos-columnas">
        <div class="contenedor-grafico">

            <P class="porcentaje"> {{ porcentaje }}%</P>

        <CircleProgress 
        :percent="porcentaje"
        :size="235"
        :border-width="25"
        :border-bg-width="25"
        />
        </div>

        <div class="contenedor-presupuesto">
            <button
            type="button"
             class="reset-app"
             @click="$emit('reset-app')"
             >
                Resetear App
            </button>

            <p>
                <span>Presupuesto:</span>
                {{ formatearCantidad(presupuesto) }}
            </p>

            <p>
                <span>Disponible:</span>
                {{ formatearCantidad(disponible) }}
            </p>

            <p>
                <span>Gastado:</span>
                {{  formatearCantidad(gastado) }}
            </p>


        </div>
    </div>
</template>

<style scoped>

    .contenedor-grafico{
        position: relative;
    }

    .porcentaje{
        position: absolute;
        margin: auto;
        top: calc(50% - 1.5rem);
        left: 0;
        right: 0;
        text-align: center;
        font-size: 4.5rem;
        font-weight: bold;
        color: var(--azul);
        z-index: 100;
    }

    .dos-columnas{
        display: flex;
        flex-direction: column;
    }

    .dos-columnas > :first-child{
        margin-bottom: 3rem;
    }

    @media (min-width: 768px) {
        .dos-columnas{
            flex-direction: row;
            gap: 4rem;
            align-items: center;
        }

        .dos-columnas > :first-child{
        margin-bottom: 0rem;
    }
    }

    .reset-app{
        background-color: #DB2777;
        border: none;
        padding: 1rem;
        width: 100%;
        color: var(--blanco);
        font-weight: 900;
        text-transform: uppercase;
        border-radius: 1rem;
        transition-property: background-color;
        transition-duration: 300ms;
    }
    .reset-app:hover{
        cursor: pointer;
        background-color: #b4165d;
    }

    .contenedor-presupuesto{
        width: 100%;
    }

    .contenedor-presupuesto p{
        font-size: 2.4rem;
        text-align: center;
    }

    @media (min-width: 768px) {
        .contenedor-presupuesto p{
        font-size: 2.4rem;
        text-align: left;
        color: var(--gris-oscuro);
    }
    }
    .contenedor-presupuesto span{
        font-weight: 900;
        color: var(--azul);
    }

</style>