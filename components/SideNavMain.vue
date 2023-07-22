<template>
  <div
    id="SideNavMain"
    :class="route.fullPath === '/' ? 'lg:w-[310px]' : 'lg:w-[220px]'"
    class="fixed z-20 bg-white pt-[70px] h-full lg:border-r-0 border-r w-[75px] overflow-auto"
  >
    <div class="lg:w-full w-[55px] mx-auto">
      <NuxtLink to="/">
        <MenuItem iconString="推荐" colorString="#F02C56" sizeString="30" />
      </NuxtLink>
      <MenuItem iconString="关注" colorString="#000000" sizeString="30" />
      <MenuItem iconString="喜欢" colorString="#000000" sizeString="30" />

      <div class="border-b lg:ml-2 mt-2" />
      <div
        class="lg:block hidden text-xs text-gray-600 font-semibold pt-4 pb-2 px-2"
      >
        推荐联系人
      </div>
      <div class="lg:hidden block pt-3" />

      <div
        v-if="$generalStore.suggested"
        v-for="sug in $generalStore.suggested"
      >
        <div @click="isLoggedIn(sug)" class="cursor-pointer">
          <MenuItemFollow :user="sug" />
        </div>
      </div>

      <button class="lg:block hidden text-[#f02c56c0] pt-1.5 pl-2 text-[13px]">
        查看更多
      </button>

      <div class="border-b lg:ml-2 mt-2" />
      <div
        class="lg:block hidden text-xs text-gray-600 font-semibold pt-4 pb-2 px-2"
      >
        关注我的人
      </div>
      <div class="lg:hidden block pt-3" />

      <div
        v-if="$generalStore.following"
        v-for="fol in $generalStore.following"
      >
        <div @click="isLoggedIn(fol)" class="cursor-pointer">
          <MenuItemFollow :user="fol" />
        </div>
      </div>

      <button class="lg:block hidden text-[#f02c56c0] pt-1.5 pl-2 text-[13px]">
        查看全部
      </button>

      <div class="lg:block hidden border-b lg:ml-2 mt-2" />

      <div class="lg:block hidden text-[11px] text-gray-500">
        <div class="pt-4 px-2">2023 © 抖音</div>
        <div class="pt-1 px-2">京ICP备16016397号-3</div>
        <div class="pt-1 px-2">网络文化许可证-京网文-（2022）0938-030号</div>
        <div class="pt-1 px-2">互联网宗教信息服务许可证 京（2022）000005</div>
      </div>

      <div class="pb-14" />
    </div>
  </div>
</template>

<script setup>
const { $generalStore, $userStore } = useNuxtApp();
const route = useRoute();
const router = useRouter();

const isLoggedIn = (fol) => {
  if (!$userStore.id) {
    $generalStore.isLoginOpen = true;
    return;
  }
  setTimeout(() => router.push(`/profile/${fol.id}`), 200);
};
</script>
