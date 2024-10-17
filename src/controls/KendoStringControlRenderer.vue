<script setup lang="ts">
import {computed} from 'vue';
import {Input} from '@progress/kendo-vue-inputs';
import {RendererProps, useJsonFormsControl} from '@jsonforms/vue';
import {ControlElement} from "@jsonforms/core";
import {Error, Label} from "@progress/kendo-vue-labels";
import {FieldWrapper} from "@progress/kendo-vue-form";

const props = defineProps<RendererProps<ControlElement>>();

const label = computed(() => control.value.label || '');
const hasErrors = computed(() =>  control.value.errors !== '' );
const appliedOptions = computed(() => control.value.uischema.options || {});

// Get the control state from JSON Forms
const {control, handleChange} = useJsonFormsControl(props);

// Watch for changes in input
const onChange = (e: HTMLInputElement) => {
  handleChange(control.value.path, e.target.value);
};
</script>

<template>
  <FieldWrapper v-if="control.visible" class="mb-4">
    <Label :editor-id="control.id" :editor-valid="!hasErrors" :disabled="!control.enabled">{{ label }}</Label>
    <Input
        :id="control.id"
        :disabled="!control.enabled"
        :placeholder="appliedOptions?.placeholder"
        :valid="!hasErrors"
        :value="control.data"
        @input="onChange"
    />
    <error v-if="hasErrors">
      {{control.errors}}
    </error>
  </FieldWrapper>
</template>
