<script setup lang="ts">
import BreadCrumbs from "@/components/BreadCrumbs.vue";
import AccordionPanel from "@/components/AccordionPanel.vue";

import {JsonForms, JsonFormsChangeEvent} from "@jsonforms/vue";
import {vanillaRenderers,} from "@jsonforms/vue-vanilla";
import {ref} from "vue";
import NextButton from "@/components/NextButton.vue";

type FormData = {
  forename?: string;
  surname?: string;
  birthdate?: string; // Stored as a string in the form of a date
  email?: string;
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
              custom: ({ data }: { data: FormData }): boolean => {
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
    <div class="profile-details__content">
      <AccordionPanel title="Details" ariaTitle="Details">
        <json-forms
            :data="data"
            :renderers="Object.freeze(layoutRenderers)"
            :schema="schema"
            :uischema="uiSchema"
            @change="onChange"
        />
      </AccordionPanel>
    </div>
    <div class="profile-details__actions">
      <div class="profile-details__actions-content">
        <NextButton />
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
