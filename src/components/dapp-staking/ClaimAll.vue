<template>
  <div v-if="currentAccount && isEnableIndividualClaim" class="widget-container">
    <div class="title">
      {{ $t('dappStaking.unclaimedRewards') }}
      <IconTooltip>
        {{ $t('dappStaking.unclaimedRewardsTooltip') }}
      </IconTooltip>
    </div>
    <div class="widget-content">
      <span class="text--title">&nbsp;</span>
      <Button
        :small="true"
        :primary="true"
        :disabled="batchTxs.length === 0 || isLoading"
        class="button"
        @click="claimAll"
      >
        {{ $t('dappStaking.claim') }}
      </Button>
    </div>
  </div>
</template>

<script lang="ts">
import { fasMoneyCheckAlt } from '@quasar/extras/fontawesome-v5';
import Button from 'src/components/common/Button.vue';
import IconTooltip from 'components/common/IconTooltip.vue';
import { useAccount, useClaimAll } from 'src/hooks';
import { defineComponent } from 'vue';

export default defineComponent({
  components: {
    Button,
    IconTooltip,
  },
  setup() {
    const { claimAll, batchTxs, isLoading, isEnableIndividualClaim } = useClaimAll();
    const { currentAccount } = useAccount();

    return {
      isEnableIndividualClaim,
      fasMoneyCheckAlt,
      claimAll,
      batchTxs,
      isLoading,
      currentAccount,
    };
  },
});
</script>

<style lang="scss" scoped>
@use 'src/components/dapp-staking/styles/user-rewards-widget.scss';
</style>
