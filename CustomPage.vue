<template>
  <q-page>
    <div class="text-center text-secondary q-ma-lg for-desktop soulmaze">
      <h2 class="q-ma-none">select components</h2>
    </div>
    <div class="text-center text-secondary q-ma-lg for-mobile soulmaze">
      <h4 class="q-ma-none">select components</h4>
    </div>
    <!-- CARDS -->
    <div>
      <div class="row justify-center">
        <!-- CPU -->
        <q-card square class="col-md-2 bg-secondary q-ma-sm" style="max-width: 15rem;">
          <q-card-section>
            <q-select v-model="selectedCpu" :options="optionsCpu" bg-color="secondary" color="secondary"
              option-label="model" option-value="id" dense options-dark options-dense outlined square></q-select>
          </q-card-section>
          <q-card-section v-if="selectedCpuInfo">
            <img class="fit" :src="selectedCpuInfo.img" alt="">
            <p class="text-center text-primary text-h5 text-weight-bold q-ma-none q-mb-sm">{{ selectedCpuInfo.type }}</p>
            <p class="text-center text-primary text-subtitle q-ma-none">{{ selectedCpuInfo.brand }} {{
              selectedCpuInfo.model }}</p>
            <p class="text-center text-primary text-subtitle q-ma-none">{{ formatCurrency(selectedCpuInfo.price) }}</p>
          </q-card-section>
          <q-card-actions></q-card-actions>
        </q-card>
        <!-- GPU -->
        <q-card square class="col-md-2 bg-secondary q-ma-sm" style="max-width: 15rem;">
          <q-card-section>
            <q-select dense square color="secondary" bg-color="secondary" outlined options-dark options-dense
              v-model="selectedGpu" :options="optionsGpu" option-value="id" option-label="model"></q-select>
          </q-card-section>
          <q-card-section v-if="selectedGpuInfo">
            <img class="fit" :src="selectedGpuInfo.img" alt="">
            <p class="text-center text-primary text-h5 text-weight-bold q-ma-none q-mb-sm">{{ selectedGpuInfo.type }} </p>
            <p class="text-center text-primary text-subtitle q-ma-none"> {{ selectedGpuInfo.brand }} {{
              selectedGpuInfo.model }} </p>
            <p class="text-center text-primary text-subtitle q-ma-none">{{ formatCurrency(selectedGpuInfo.price) }} </p>
          </q-card-section>
          <q-card-actions></q-card-actions>
        </q-card>
        <!-- MOBO -->
        <q-card square class="col-md-2 bg-secondary q-ma-sm" style="max-width: 15rem;">
          <q-card-section>
            <q-select dense square color="secondary" bg-color="secondary" outlined options-dark options-dense
              v-model="selectedMobo" :options="optionsMobo" option-value="id" option-label="model"></q-select>
          </q-card-section>
          <q-card-section v-if="selectedMoboInfo">
            <img class="fit" :src="selectedMoboInfo.img" alt="">
            <p class="text-center text-primary text-h5 text-weight-bold q-ma-none q-mb-sm">{{ selectedMoboInfo.type }}</p>
            <p class="text-center text-primary text-subtitle q-ma-none">{{ selectedMoboInfo.brand }} {{
              selectedMoboInfo.model }}</p>
            <p class="text-center text-primary text-subtitle q-ma-none">{{ formatCurrency(selectedMoboInfo.price) }}</p>
          </q-card-section>
          <q-card-actions></q-card-actions>
        </q-card>

        <!-- POWERSUPPLY -->
        <q-card square class="col-md-2 bg-secondary q-ma-sm" style="max-width: 15rem;">
          <q-card-section>
            <q-select dense square color="secondary" bg-color="secondary" outlined options-dark options-dense
              v-model="selectedPowersupply" :options="optionsPowersupply" option-value="id"
              option-label="model"></q-select>
          </q-card-section>
          <q-card-section v-if="selectedPowersupplyInfo">
            <img class="fit" :src="selectedPowersupplyInfo.img" alt="">
            <p class="text-center text-primary text-h5 text-weight-bold q-ma-none q-mb-sm">{{ selectedPowersupplyInfo.type
            }}
            </p>
            <p class="text-center text-primary text-subtitle q-ma-none"> {{ selectedPowersupplyInfo.brand }} {{
              selectedPowersupplyInfo.model }} </p>
            <p class="text-center text-primary text-subtitle q-ma-none">{{ formatCurrency(selectedPowersupplyInfo.price)
            }} </p>
          </q-card-section>
          <q-card-actions></q-card-actions>
        </q-card>
        <!-- RAM -->
        <q-card square class="col-md-2 bg-secondary q-ma-sm" style="max-width: 15rem;">
          <q-card-section>
            <q-select dense square color="secondary" bg-color="secondary" outlined options-dark options-dense
              v-model="selectedRam" :options="optionsRam" option-value="id" option-label="model"></q-select>
          </q-card-section>
          <q-card-section v-if="selectedRamInfo">
            <img class="fit" :src="selectedRamInfo.img" alt="">
            <p class="text-center text-primary text-h5 text-weight-bold q-ma-none q-mb-sm">{{ selectedRamInfo.type
            }}
            </p>
            <p class="text-center text-primary text-subtitle q-ma-none"> {{ selectedRamInfo.brand }} {{
              selectedRamInfo.model }} </p>
            <p class="text-center text-primary text-subtitle q-ma-none">{{ formatCurrency(selectedRamInfo.price) }} </p>
          </q-card-section>
          <q-card-actions></q-card-actions>
        </q-card>
      </div>
    </div>
    <!-- DIALOG -->
    <div>
      <q-dialog v-model="viewDetailsBtn" persistent :maximized="maximizedToggle = true" transition-show="slide-up"
        transition-hide="slide-down">
        <q-card class="bg-primary text-white">
          <q-bar>
            <q-space />
            <q-btn dense flat icon="close" v-close-popup>
              <q-tooltip class="bg-white text-primary">Close</q-tooltip>
            </q-btn>
          </q-bar>

          <q-card-section>
            <div class="text-h2 soulmaze text-center text-secondary q-mb-sm">PC DETAILS</div>
            <div class="text-h5  text-center text-secondary text-weight-bold text-uppercase">PROFILE: CUSTOM</div>
          </q-card-section>
          <q-card-section class="q-px-xl row justify-start">
            <!-- CPU -->
            <div class="col-12 col-md-6">
              <q-item class="text-secondary row justify-center">
                <q-item-section top class="q-ml-none col-auto">
                  <img width="140" :src="selectedCpu.img">
                </q-item-section>
                <q-item-section class="col-12 col-md-8 row justify-center">
                  <div>
                    <div class="col-md-12">
                      <q-item-label class="text-uppercase text-caption text-weight-bold">Part: {{ selectedCpu.type
                      }}</q-item-label>
                    </div>
                    <div class="col-md-12">
                      <q-item-label class="text-uppercase text-caption text-weight-bold">Brand: {{ selectedCpu.brand
                      }}</q-item-label>
                    </div>
                    <div class="col-md-12">
                      <q-item-label class="text-uppercase text-caption text-weight-bold">Model: {{ selectedCpu.model
                      }}</q-item-label>
                    </div>
                    <div class="col-md-12 q-mb-xs">
                      <q-item-label class="text-uppercase text-caption text-weight-bold">Rating: {{
                        `${selectedCpu.performanceRating}/10
                        `}}</q-item-label>
                    </div>
                    <div class="col-md-8">
                      <q-item-label class="text-secondary" caption>{{ selectedCpu.description }}</q-item-label>
                    </div>
                  </div>
                </q-item-section>
              </q-item>
            </div>
            <!-- GPU -->
            <div class="col-12 col-md-6">
              <q-item class="text-secondary row justify-center">
                <q-item-section top class="q-ml-none col-auto">
                  <img width="140" :src="selectedGpu.img">
                </q-item-section>
                <q-item-section class="col-12 col-md-8 row justify-center">
                  <div>
                    <div class="col-md-12">
                      <q-item-label class="text-uppercase text-caption text-weight-bold">Part: {{ selectedGpu.type
                      }}</q-item-label>
                    </div>
                    <div class="col-md-12">
                      <q-item-label class="text-uppercase text-caption text-weight-bold">Brand: {{ selectedGpu.brand
                      }}</q-item-label>
                    </div>
                    <div class="col-md-12">
                      <q-item-label class="text-uppercase text-caption text-weight-bold">Model: {{ selectedGpu.model
                      }}</q-item-label>
                    </div>
                    <div class="col-md-12 q-mb-xs">
                      <q-item-label class="text-uppercase text-caption text-weight-bold">Rating: {{
                        `${selectedGpu.performanceRating}/10
                        `}}</q-item-label>
                    </div>
                    <div class="col-md-8">
                      <q-item-label class="text-secondary" caption>{{ selectedGpu.description }}</q-item-label>
                    </div>
                  </div>
                </q-item-section>
              </q-item>
            </div>
            <!-- MOTHERBOARD -->
            <div class="col-12 col-md-6">
              <q-item class="text-secondary row justify-center">
                <q-item-section top class="q-ml-none col-auto">
                  <img width="140" :src="selectedMobo.img">
                </q-item-section>
                <q-item-section class="col-12 col-md-8 row justify-center">
                  <div>
                    <div class="col-md-12">
                      <q-item-label class="text-uppercase text-caption text-weight-bold">Part: {{ selectedMobo.type
                      }}</q-item-label>
                    </div>
                    <div class="col-md-12">
                      <q-item-label class="text-uppercase text-caption text-weight-bold">Brand: {{ selectedMobo.brand
                      }}</q-item-label>
                    </div>
                    <div class="col-md-12">
                      <q-item-label class="text-uppercase text-caption text-weight-bold">Model: {{ selectedMobo.model
                      }}</q-item-label>
                    </div>
                    <div class="col-md-12 q-mb-xs">
                      <q-item-label class="text-uppercase text-caption text-weight-bold">Rating: {{
                        `${selectedMobo.performanceRating}/10
                        `}}</q-item-label>
                    </div>
                    <div class="col-md-8">
                      <q-item-label class="text-secondary" caption>{{ selectedMobo.description }}</q-item-label>
                    </div>
                  </div>
                </q-item-section>
              </q-item>
            </div>
            <!-- POWERSUPPLY -->
            <div class="col-12 col-md-6">
              <q-item class="text-secondary row justify-center">
                <q-item-section top class="q-ml-none col-auto">
                  <img width="140" :src="selectedPowersupply.img">
                </q-item-section>
                <q-item-section class="col-12 col-md-8 row justify-center">
                  <div>
                    <div class="col-md-12">
                      <q-item-label class="text-uppercase text-caption text-weight-bold">Part: {{ selectedPowersupply.type
                      }}</q-item-label>
                    </div>
                    <div class="col-md-12">
                      <q-item-label class="text-uppercase text-caption text-weight-bold">Brand: {{
                        selectedPowersupply.brand
                      }}</q-item-label>
                    </div>
                    <div class="col-md-12">
                      <q-item-label class="text-uppercase text-caption text-weight-bold">Model: {{
                        selectedPowersupply.model
                      }}</q-item-label>
                    </div>
                    <div class="col-md-12 q-mb-xs">
                      <q-item-label class="text-uppercase text-caption text-weight-bold">Rating: {{
                        `${selectedPowersupply.performanceRating}/10
                        `}}</q-item-label>
                    </div>
                    <div class="col-md-8">
                      <q-item-label class="text-secondary" caption>{{ selectedPowersupply.description }}</q-item-label>
                    </div>
                  </div>
                </q-item-section>
              </q-item>
            </div>
            <!-- RAM -->
            <div class="col-12 col-md-6">
              <q-item class="text-secondary row justify-center">
                <q-item-section top class="q-ml-none col-auto">
                  <img width="140" :src="selectedRam.img">
                </q-item-section>
                <q-item-section class="col-12 col-md-8 row justify-center">
                  <div>
                    <div class="col-md-12">
                      <q-item-label class="text-uppercase text-caption text-weight-bold">Part: {{ selectedRam.type
                      }}</q-item-label>
                    </div>
                    <div class="col-md-12">
                      <q-item-label class="text-uppercase text-caption text-weight-bold">Brand: {{ selectedRam.brand
                      }}</q-item-label>
                    </div>
                    <div class="col-md-12">
                      <q-item-label class="text-uppercase text-caption text-weight-bold">Model: {{ selectedRam.model
                      }}</q-item-label>
                    </div>
                    <div class="col-md-12 q-mb-xs">
                      <q-item-label class="text-uppercase text-caption text-weight-bold">Rating: {{
                        `${selectedRam.performanceRating}/10
                        `}}</q-item-label>
                    </div>
                    <div class="col-md-8">
                      <q-item-label class="text-secondary" caption>{{ selectedRam.description }}</q-item-label>
                    </div>
                  </div>
                </q-item-section>
              </q-item>
            </div>
          </q-card-section>
        </q-card>
      </q-dialog>
    </div>
    <div class="row justify-between mont3 q-mt-md select">
      <div class="col-12 col-md-6 column ">
        <div square class="bg-primary q-ma-sm">
          <div class="q-mb-md">
            <h4 class="text-secondary text-weight-bold text-italic q-ma-none">PC TYPE:</h4>
            <q-select dense square color="secondary" bg-color="secondary" outlined options-dark options-dense
              v-model="select" :options="options">
              <template v-slot:append>
                <q-avatar>
                  <img src="../assets/img/logo.png">
                </q-avatar>
              </template>
            </q-select>
          </div>
          <div class="q-mb-md">
            <h4 class=" text-secondary text-weight-bold text-italic q-ma-none">PERFORMANCE:</h4>
            <q-linear-progress track-color="secondary" stripe square size="30px" color="secondary"
              :value="overallProgress" class="q-mt-sm" />

          </div>
          <div class="q-mb-md">
            <h4 class=" text-secondary text-weight-bold text-italic q-ma-none">PRICE: {{ price }}</h4>
          </div>

        </div>
      </div>
      <div class="col-12 col-md-auto q-pa-none q-mb-lg bg-secondary">
        <q-card style="max-width: 17rem;" square flat class="bg-primary text-secondary q-ma-sm">
          <q-card-section class="text-center">
            <img class="fit" src="../assets/img/pc3.png" alt="">
            <q-btn class="bg-primary text-secondary text-weight-bold q-mt-sm" flat label="VIEW DETAILS"
              @click="viewDetails" />
          </q-card-section>
        </q-card>
      </div>
    </div>
    <q-dialog persistent auto v-model="showError">
      <q-card style="height: 400px;width: 350px;" class="bg-secondary">
        <q-card-section class="row items-center q-pb-none">
          <div class="text-h6 text-weight-bold">MISMATCH!</div>
          <q-space />
          <q-btn icon="close" flat round dense @click="closePopUp" v-close-popup />
        </q-card-section>
        <q-separator class="q-mt-sm" />
        <q-card-section class="text-center bg-dark ">
          <div class="q-mb-sm text-secondary text-h5 mont q-ma-none">
            Compatibility Issues Found
            Choose another component
          </div>
          <img width="200" src="../assets/img/GPU/1.png" alt="">
        </q-card-section>
      </q-card>
    </q-dialog>
  </q-page>
</template>

<script setup>
import { ref, computed, watch, onMounted } from 'vue';
import pcPartsData from '../Data/pcParts2.json';
import { useRouter } from 'vue-router';


//CPU
const selectedCpu = ref(pcPartsData.custom.cpu[0]);
const optionsCpu = pcPartsData.custom.cpu;
const selectedCpuInfo = computed(() => {
  return pcPartsData.custom.cpu.find(cpu => cpu.id === selectedCpu.value.id);
});

//GPU
const selectedGpu = ref(pcPartsData.custom.gpu[0]);
const optionsGpu = pcPartsData.custom.gpu;
const selectedGpuInfo = computed(() => {
  return pcPartsData.custom.gpu.find(gpu => gpu.id === selectedGpu.value.id);
});

//MOBO
const selectedMobo = ref(pcPartsData.custom.motherboard[0]);
const optionsMobo = pcPartsData.custom.motherboard;
const selectedMoboInfo = computed(() => {
  return pcPartsData.custom.motherboard.find(mobo => mobo.id === selectedMobo.value.id);
});

//POWERSUPPLY
const selectedPowersupply = ref(pcPartsData.custom.powersupply[0]);
const optionsPowersupply = pcPartsData.custom.powersupply;
const selectedPowersupplyInfo = computed(() => {
  return pcPartsData.custom.powersupply.find(powersupply => powersupply.id === selectedPowersupply.value.id);
});

//RAM
const selectedRam = ref(pcPartsData.custom.ram[0]);
const optionsRam = pcPartsData.custom.ram;
const selectedRamInfo = computed(() => {
  return pcPartsData.custom.ram.find(ram => ram.id === selectedRam.value.id);
});

//CALCULATE PRICE
const price = computed(() => {
  let totalPrice = selectedCpuInfo.value.price + selectedGpuInfo.value.price + selectedMobo.value.price + selectedPowersupply.value.price + selectedRam.value.price
  totalPrice = totalPrice.toLocaleString('en-US', { style: 'currency', currency: 'PHP' });
  return totalPrice
})

//CALCULATE PROGRESS
const overallProgress = computed(() => {
  const totalRating = selectedCpuInfo.value.performanceRating + selectedGpuInfo.value.performanceRating + selectedMobo.value.performanceRating + selectedPowersupply.value.performanceRating + selectedRam.value.performanceRating;
  const maxRating = 50;

  const overallProgress = totalRating / maxRating;

  const minProgress = 0;
  const maxProgress = 1.0;
  const overallProgressNormalized = minProgress + (maxProgress - minProgress) * overallProgress;

  return overallProgressNormalized;
});

//PRICE FORMATTER HELPER FUNCTION
function formatCurrency(value) {
  return value.toLocaleString('en-US', { style: 'currency', currency: 'PHP' });
}

//OPEN VIEW DETAILS DIALOG
const viewDetailsBtn = ref(false);
const viewDetails = () => {
  viewDetailsBtn.value = true;
};


//SELECT OPTIONS
const select = ref('Custom')
const options = [
  "Work/Studies", "Gaming", "Editing", "Custom"
]

// REDIRECT TO THE CUSTOM PAGE IF CUSTOM IS SELECTED
const router = useRouter()
watch(select, (newValue) => {
  if (newValue === 'Work/Studies' || newValue === 'Gaming' || newValue === 'Editing') {
    router.push({ path: '/build', query: { option: select.value } });
  }
});

//ERRORS
const showError = ref(false)
const isSelectionValid = computed(() => {
  return selectedCpu.value.socket === selectedMobo.value.compatibility;
});

watch(isSelectionValid, (isValid) => {
  showError.value = !isValid;
});

const closePopUp = () => {
  selectedCpu.value = pcPartsData.custom.cpu[0];
  selectedMobo.value = pcPartsData.custom.motherboard[0];
}

</script>
