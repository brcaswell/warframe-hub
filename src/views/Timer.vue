<template>
  <div class="timers">
    <b-container fluid class="grid">
      <b-row ref="timerComponentGrid" v-packery="{ itemSelector: '.packery-item', percentPosition: true }">
        <timer v-if="componentState.earth.display" :time="worldstate.earthCycle" location="Earth" />
        <timer v-if="componentState.cetus.display" :time="worldstate.cetusCycle" location="Cetus" />
        <timer v-if="componentState.vallis.display" :time="worldstate.vallisCycle" location="Vallis" />
        <sentientOutposts
          v-if="componentState.sentientoutposts.display"
          :sentientOutposts="worldstate.sentientOutposts"
        />
        <reset v-if="componentState.reset.display" />
        <construction v-if="componentState.construction.display" :construction="worldstate.constructionProgress" />
        <deals v-if="componentState.darvo.display" :deals="worldstate.dailyDeals" />
        <news v-if="componentState.news.display" :news="worldstate.news" />
        <acolytes v-if="componentState.acolytes.display" :acolytes="worldstate.persistentEnemies" />
        <events v-if="componentState.event.display" :events="worldstate.events" />
        <alerts v-if="componentState.alerts.display" :alerts="worldstate.alerts" />
        <invasions v-if="componentState.invasions.display" :invasions="worldstate.invasions" />
        <nightwave v-if="componentState.nightwave.display" :nightwave="worldstate.nightwave" />
        <conclave v-if="componentState.conclave.display" :conclave="worldstate.conclaveChallenges" />
        <sortie v-if="componentState.sortie.display" :sortie="worldstate.sortie" />
        <arbitration v-if="componentState.arbitration.display" :arbitration="worldstate.arbitration" />
        <fissures v-if="componentState.fissures.display" :fissures="worldstate.fissures" />
        <kuvas v-if="componentState.kuvas.display" :kuvas="worldstate.kuva" />
        <bounty v-if="componentState.bounties.display" :syndicate="ostron" :type="$t('timer.ostron')" />
        <bounty v-if="componentState['solaris-bounties'].display" :syndicate="solaris" :type="$t('timer.solaris')" />
        <sales v-if="componentState.deals.display" :sales="worldstate.flashSales" />
        <void-trader v-if="componentState.baro.display" :voidTrader="worldstate.voidTrader" />
        <bounty v-if="componentState['hivemind-bounties'].display" :syndicate="hivemind" :type="$t('timer.hivemind')" />
      </b-row>
    </b-container>
  </div>
</template>

<script>
import { mapState, mapGetters } from 'vuex';
import AlertPanel from '@/components/panels/AlertPanel.vue';
import NewsPanel from '@/components/panels/NewsPanel.vue';
import TimePanel from '@/components/panels/TimePanel.vue';
import ResetPanel from '@/components/panels/ResetPanel.vue';
import SortiePanel from '@/components/panels/SortiePanel.vue';
import ArbitrationPanel from '@/components/panels/ArbitrationPanel.vue';
import AcolytesPanel from '@/components/panels/AcolytesPanel.vue';
import FissuresPanel from '@/components/panels/FissuresPanel.vue';
import KuvaPanel from '@/components/panels/KuvaPanel.vue';
import BountyPanel from '@/components/panels/BountyPanel.vue';
import InvasionsPanel from '@/components/panels/InvasionsPanel.vue';
import EventsPanel from '@/components/panels/EventsPanel.vue';
import DarvoDealsPanel from '@/components/panels/DarvoDealsPanel.vue';
import SalesPanel from '@/components/panels/SalesPanel.vue';
import VoidTraderPanel from '@/components/panels/VoidTraderPanel.vue';
import NightwavePanel from '@/components/panels/NightwavePanel.vue';
import ConstructionPanel from '@/components/panels/ConstructionPanel.vue';
import SentientOutpostsPanel from '@/components/panels/SentientOutpostsPanel.vue';
import ConclavePanel from '@/components/panels/ConclavePanel.vue';

export default {
  name: 'timers',
  components: {
    alerts: AlertPanel,
    news: NewsPanel,
    timer: TimePanel,
    reset: ResetPanel,
    sortie: SortiePanel,
    arbitration: ArbitrationPanel,
    acolytes: AcolytesPanel,
    fissures: FissuresPanel,
    kuvas: KuvaPanel,
    bounty: BountyPanel,
    invasions: InvasionsPanel,
    events: EventsPanel,
    deals: DarvoDealsPanel,
    sales: SalesPanel,
    'void-trader': VoidTraderPanel,
    nightwave: NightwavePanel,
    construction: ConstructionPanel,
    sentientOutposts: SentientOutpostsPanel,
    conclave: ConclavePanel,
  },
  data() {
    return {
      components: {},
    };
  },
  methods: {
    track() {
      this.$ga.page('/');
    },
  },
  computed: {
    ...mapState({
      componentState: 'components',
      gridState: 'grid',
    }),
    ...mapGetters({
      worldstate: 'worldstate',
      ostron: 'ostronSyndicate',
      solaris: 'solarisSyndicate',
      hivemind: 'hivemindSyndicate',
    }),
  },
};
</script>
<style>
/* Saved for testing purposes */
/*
.grid-item {
  border: 1px dotted #000;
  background-color: rgb(146, 146, 146);
}
*/
</style>
