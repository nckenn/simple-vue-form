<script setup lang="ts">
import {computed} from 'vue';
import {RendererProps, useJsonFormsControl} from '@jsonforms/vue';
import {ControlElement} from "@jsonforms/core";
import {Error, Label} from "@progress/kendo-vue-labels";
import {FieldWrapper} from "@progress/kendo-vue-form";
import {DatePicker, DatePickerChangeEvent} from "@progress/kendo-vue-dateinputs";
import dayjs from "dayjs";

const props = defineProps<RendererProps<ControlElement>>();

const label = computed(() => control.value.label || '');
const hasErrors = computed(() =>  control.value.errors !== '' );
const appliedOptions = computed(() => control.value.uischema.options || {});

// Get the control state from JSON Forms
const {control, handleChange} = useJsonFormsControl(props);


const inputValue = () => {
  const value = control.value.data;
  return value ? dayjs(control.value.data).toDate() : null;
}

// Watch for changes in input
const onChange = (e: DatePickerChangeEvent) => {
  const target = e.target as HTMLInputElement;
  const date = dayjs(target.value).format('YYYY-MM-DD');
  handleChange(control.value.path, date);
};
</script>

<template>
  <FieldWrapper v-if="control.visible" class="mb-4">
    <Label :editor-id="control.id" :editor-valid="!hasErrors" :disabled="!control.enabled">{{ label }}</Label>
    <DatePicker
        :id="control.id"
        :disabled="!control.enabled"
        :placeholder="appliedOptions?.placeholder"
        :valid="!hasErrors"
        :value="inputValue()"
        :format="'yyyy-MM-dd'"
        @change="onChange"
    />
    <error v-if="hasErrors">
      {{control.errors}}
    </error>
  </FieldWrapper>
</template>
