<template>
    <v-container>
      <v-row>
        <v-col cols="4">
          <v-tabs v-model="tab" vertical>
              <v-tab v-for="tab in tabs" :key="tab.tabName">
                  {{ tab.tabName }}
              </v-tab>
          </v-tabs>
        </v-col>
        <v-col cols="8">
          <v-tabs-items v-model="tab">
              <v-tab-item v-for="tab in tabs" :key="tab.tabName">
                  <v-card flat>
                      <component v-bind:is="tab.component"></component>
                  </v-card>
              </v-tab-item>
          </v-tabs-items>
        </v-col>
      </v-row>
    </v-container>
</template>

<script>
import IdTab from './modules/IdTab.vue'
import NameTab from './modules/NameTab.vue'
import PasswordTab from './modules/PasswordTab.vue'
import EmailTab from './modules/EmailTab.vue'
import familyNameTab from './modules/FamilyNameTab.vue'
import lastNameTab from './modules/LastNameTab.vue'
import famNameKanaTab from './modules/FamNameKanaTab.vue'
import lastNameKanaTab from './modules/LastNameKanaTab.vue'
import zipCodeTab from './modules/ZipCodeTab.vue'
import senderZipCodeTab from './modules/SenderZipCodeTab.vue'
import address1Tab from './modules/Address1Tab.vue'
import address2Tab from './modules/Address2Tab.vue'
import contactNumberTab from './modules/ContactNumberTab.vue'
import restaurantTab from './modules/RestaurantTab.vue'
import courseTab from './modules/CourseTab.vue'
import capacityTab from './modules/CapacityTab.vue'
import googleMapTab from './modules/GoogleMapTab.vue'
import shippingDateTab from './modules/ShippingDateTab.vue'
import arrivalDateTab from './modules/ArrivalDateTab.vue'
import fishSpeciesTab from './modules/FishSpeciesTab.vue'
import courseNameTab from './modules/CourseNameTab.vue'
import recipientNameTab from './modules/RecipientNameTab.vue'
import recipientNameKanaTab from './modules/RecipientNameKanaTab.vue'
import consignorCodeTab from './modules/ConsignorCodeTab.vue'
import deliverySizeTab from './modules/DeliverySizeTab.vue'
import storageTemperatureTab from './modules/StorageTemperatureTab.vue'
import itemCodeTab from './modules/ItemCodeTab.vue'
import itemNameTab from './modules/ItemNameTab.vue'
import senderNameTab from './modules/SenderNameTab.vue'
import senderAddressTab from './modules/SenderAddressTab.vue'
import senderAddress2Tab from './modules/SenderAddress2Tab.vue'
import destinationAddressTab from './modules/DestinationAddressTab.vue'
import destinationAddress2Tab from './modules/DestinationAddress2Tab.vue'
import destinationPhoneNumberTab from './modules/DestinationPhoneNumberTab.vue'
import senderPhoneNumberTab from './modules/SenderPhoneNumberTab.vue'
import senderEmailTab from './modules/SenderEmailTab.vue'
import recipientZipCode from './modules/RecipientZipCodeTab.vue'
import recipientAddress1 from './modules/RecipientAddress1Tab.vue'
import recipientAddress2 from './modules/RecipientAddress2Tab.vue'
import recipientPNumber from './modules/RecipientPNumberTab.vue'
import recipientEmail from './modules/RecipientEmailTab.vue'
import operation from './modules/OperationTab.vue'
import emailMagazine from './modules/EmailMagazineTab.vue'

  export default {
    data: () => ({
      tab: null,
      tabs: [
        { tabName: 'id', component: IdTab },
        {
          tabName: 'name',
          component: NameTab
        },
        {
          tabName: 'password',
          component: PasswordTab
        },
        {
          tabName: 'email',
          component: EmailTab
        },
        {
          tabName: 'familyName',
          component: familyNameTab
        },
        {
          tabName: 'lastName',
          component: lastNameTab
        },
        {
          tabName: 'familyNameKana',
          component: famNameKanaTab
        },
        {
          tabName: 'lastNameKana',
          component: lastNameKanaTab
        },
        {
          tabName: 'zipCode',
          component: zipCodeTab
        },
        {
          tabName: 'senderZipCode',
          component: senderZipCodeTab
        },
        {
          tabName: 'address1',
          component: address1Tab
        },
        {
          tabName: 'address2',
          component: address2Tab
        },
        {
          tabName: 'phoneNumber',
          component: contactNumberTab
        },
        {
          tabName: 'restaurant',
          component: restaurantTab
        },
        {
          tabName: 'course',
          component: courseTab
        },
        {
          tabName: 'capacity',
          component: capacityTab
        },
        {
          tabName: 'googlemap',
          component: googleMapTab
        },
        {
          tabName: 'shippingDate',
          component: shippingDateTab
        },
        {
          tabName: 'arrivalDate',
          component: arrivalDateTab
        },
        {
          tabName: 'fishSpecies',
          component: fishSpeciesTab
        },
        {
          tabName: 'courseName',
          component: courseNameTab
        },
        {
          tabName: 'recipientName',
          component: recipientNameTab
        },
        {
          tabName: 'recipientNameKana',
          component: recipientNameKanaTab
        },
        {
          tabName: 'consignorCode',
          component: consignorCodeTab
        },
        {
          tabName: 'deliverySize',
          component: deliverySizeTab
        },
        {
          tabName: 'storageTemperature',
          component: storageTemperatureTab
        },
        {
          tabName: 'itemCode',
          component: itemCodeTab
        },
        {
          tabName: 'itemName',
          component: itemNameTab
        },
        {
          tabName: 'fullName'
        },
        {
          tabName: 'senderName',
          component: senderNameTab
          
        },
        {
          tabName: 'senderAddress1',
          component: senderAddressTab
        },
        {
          tabName: 'senderAddress2',
          component: senderAddress2Tab
        },
        {
          tabName: 'destinationAddress1',
          component: destinationAddressTab
        },
        {
          tabName: 'destinationAddress2',
          component: destinationAddress2Tab
        },
        {
          tabName: 'destinationPhoneNumber',
          component: destinationPhoneNumberTab
        },
        {
          tabName: 'senderPhoneNumber',
          component: senderPhoneNumberTab
        },
        {
          tabName: 'senderEmail',
          component: senderEmailTab
        },
        {
          tabName: 'recipientZipCode',
          component: recipientZipCode
        },
        {
          tabName: 'recipientAddress1',
          component: recipientAddress1
        },
        {
          tabName: 'recipientAddress2',
          component: recipientAddress2
        },
        {
          tabName: 'recipientPhoneNumber',
          component: recipientPNumber
        },
        {
          tabName: 'recipientEmail',
          component: recipientEmail
        },
        {
          tabName: 'Operation',
          component: operation
        },
        {
          tabName: 'emailMagazine',
          component: emailMagazine
        }
      ],
    }),  
  }
</script>
