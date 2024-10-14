<script setup lang="ts">
import BreadCrumbs from "@/components/BreadCrumbs.vue";
import AccordionPanel from "@/components/AccordionPanel.vue";

import { JsonForms, JsonFormsChangeEvent } from "@jsonforms/vue";
import {
  defaultStyles,
  mergeStyles,
  vanillaRenderers,
} from "@jsonforms/vue-vanilla";
import {onMounted, reactive, ref, shallowRef} from "vue";

type ProfileForm = {
  forename: string;
  surname: string;
  birthdate: string;
  email: string;
}

const layoutRenderers = [
  ...vanillaRenderers
];

const schema = {
  properties: {
    forename: {
      title: "Forename(s)",
      type: "string",
    },
    surname: {
      title: "Surname",
      type: "string",
    },
    birthdate: {
      title: "Date of Birth",
      type: "string",
      format: "date"
    },
    email: {
      title: "Email Address",
      type: "string",
      format: "email"
    }
  },
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
        },
        {
          type: "Control",
          scope: "#/properties/email",
          rule: {
            effect: "SHOW",
            condition: {
              scope: "#/properties/birthdate",
              schema: {
                type: "string",
                format: "date"
              },
              // Custom function to calculate age
              test: ({ data }) => {
                if (!data.birthdate) {
                  return false;
                }
                const today = new Date();
                const birthdate = new Date(data.birthdate);
                let age = today.getFullYear() - birthdate.getFullYear();
                const monthDiff = today.getMonth() - birthdate.getMonth();
                if (monthDiff < 0 || (monthDiff === 0 && today.getDate() < birthdate.getDate())) {
                  age--;
                }
                return age >= 18;
              }
            },
          },
        },
      ],
    },
  ],
};

const data = ref<any>({
  forename: "John",
  surname: "Smith",
  email: ""
});

const onChange = (event: JsonFormsChangeEvent) => {
  data.value = event.data;
};

</script>

<template>
  <div class="profile-details">
    <BreadCrumbs />
    <span class="profile-details__title">Profile Detail</span>
    <div class="profile-details__info">
      This is the personal information you use to access and manage your account. Your email address will be used for account security, recovery, and notifications.
    </div>
    <AccordionPanel title="Details" aria-title="Details">
      <json-forms
          :data="data"
          :renderers="Object.freeze(layoutRenderers)"
          :schema="schema"
          :uischema="uiSchema"
          @change="onChange"
      />
    </AccordionPanel>
  </div>
</template>

<style scoped lang="scss">
.profile-details {
  display: flex;
  gap: 12px;
  flex-direction: column;

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
}

.horizontal-layout {
  gap: 20px;
}

</style>
