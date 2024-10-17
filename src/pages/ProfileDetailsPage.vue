<script setup lang="ts">
import BreadCrumbs from "@/components/BreadCrumbs.vue";
import AccordionPanel from "@/components/AccordionPanel.vue";

import {JsonForms, JsonFormsChangeEvent} from "@jsonforms/vue";
import {vanillaRenderers,} from "@jsonforms/vue-vanilla";
import {ref} from "vue";
import NextButton from "@/components/NextButton.vue";
import {isDateControl, isStringControl, JsonSchema, rankWith} from "@jsonforms/core";
import KendoStringControlRenderer from "@/controls/KendoStringControlRenderer.vue";
import KendoDateControlRenderer from "@/controls/KendoDateControlRenderer.vue";

const customRenderers = [
  {
    tester: rankWith(
        3,
        isStringControl,
    ), renderer: KendoStringControlRenderer
  },
  {
    tester: rankWith(
        4,
        isDateControl,
    ), renderer: KendoDateControlRenderer
  }
];

const layoutRenderers = [
  ...vanillaRenderers,
  ...customRenderers
];

const schema: JsonSchema = {
  type: "object",
  properties: {
    forename: {
      title: "Forename(s)",
      type: "string",
      minLength: 3,
    },
    surname: {
      title: "Surname",
      type: "string",
    },
    birthdate: {
      title: "Date of Birth",
      type: "string",
      format: "date",
    },
    email: {
      title: "Email Address",
      type: "string",
      format: "email",
    },
    age: {
      type: "integer",
      title: "Age",
      readOnly: true // This field will not be directly editable by the user
    },
  },
  required: ["forename", "surname", "birthdate", "email"]
};

const uiSchema = {
  type: "HorizontalLayout",
  elements: [
    {
      type: "VerticalLayout",
      elements: [
        {
          type: "Control",
          scope: "#/properties/forename",
          options: {
            placeholder: "Enter Forename",
          }
        },
        {
          type: "Control",
          scope: "#/properties/birthdate"
        }
      ],
    },
    {
      type: "VerticalLayout",
      elements: [
        {
          type: "Control",
          scope: "#/properties/surname",
          options: {
            placeholder: "Enter Surname",
          }
        },
        {
          type: "Control",
          scope: "#/properties/email",
          options: {
            placeholder: "Enter Email Address",
          },
          rule: {
            effect: "SHOW",
            condition: {
              scope: "#/properties/age",
              schema: {
                type: "integer",
                // Only show if age is 18 or greater
                minimum: 18
              },
            },
          },
        },
      ],
    },
  ],
};

const formData = ref({});

const isFormValid = ref<boolean>(false);

const onChange = (event: JsonFormsChangeEvent) => {
  const data = event.data;
  const errors = event.errors;
  console.log(errors);

  // Calculate age based on birthdate if present
  if(data?.birthdate) {
    data.age = calculateAge(data.birthdate);
  }

  // Update form data and validity state
  formData.value = data;
  // Update form validity based on errors
  isFormValid.value = errors?.length === 0;
};

const calculateAge = (birthdate: string) => {
  const today = new Date();
  const birthDate = new Date(birthdate);
  let age = today.getFullYear() - birthDate.getFullYear();
  const monthDiff = today.getMonth() - birthDate.getMonth();
  if (monthDiff < 0 || (monthDiff === 0 && today.getDate() < birthDate.getDate())) {
    age--;
  }
  return age;
}

</script>

<template>
  <div class="profile-details">
    <BreadCrumbs />
    <span class="profile-details__title">Profile Detail</span>
    <div class="profile-details__info">
      This is the personal information you use to access and manage your account. Your email address will be used for account security, recovery, and notifications.
    </div>
    <div class="profile-details__content">
      <AccordionPanel title="Details" ariaTitle="Details">
        <json-forms
            :data="formData"
            :renderers="Object.freeze(layoutRenderers)"
            :schema="schema"
            :uischema="uiSchema"
            @change="onChange"
        />
      </AccordionPanel>
    </div>
    <div class="profile-details__actions">
      <div class="profile-details__actions-content">
        <NextButton :disabled="!isFormValid"/>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.profile-details {
  display: flex;
  gap: 12px;
  flex-direction: column;
  height: calc(100vh - 78px);

  &__content {
    flex: 1;
  }

  &__title {
    font-size: 20px;
    font-weight: 700;
    line-height: 28px;
    color: #003366;
  }

  &__info {
    padding: 15px;
    border-radius: 8px;
    border: 0.2px solid #d2d7df;
    background: #E5F2FF;
    font-size: 18px;
    font-weight: 500;
    line-height: 23.4px;
    color: #003366;
  }

  &__actions {
    display: flex;
    align-items: center;
    justify-content: flex-end;
    width: 100%;
    background: #ffffff;
    height: 64px;
    padding: 10px 0;
    border-top: 0.5px solid #dbdcdc;
    position: absolute;
    bottom: 0;
    left: 0;

    &-content {
      display: flex;
      align-items: center;
      justify-content: flex-end;
      max-width: 1070px;
      margin: 0 auto;
      width: 100%;
    }
  }
}

.horizontal-layout {
  gap: 20px;
}

</style>
