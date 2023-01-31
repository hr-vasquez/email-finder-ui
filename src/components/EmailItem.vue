<template>
    <div v-if="itemCollapsed">
        <div class="grid grid-cols-[100px_1fr_100px] auto-rows-[38px] rounded-xl
        bg-gradient-to-r from-sky-500 to-indigo-800 text-white" @click="onClickItem">

            <!--Item Icon-->
            <div class="grid items-center justify-center row-span-2 h-16 w-16 rounded-full
            text-3xl text-center bg-violet-800 self-center justify-self-center">
                <span class="text-white">
                    {{emailItem.from.charAt(0).toUpperCase()}}
                </span>
            </div>

            <!--Item Subject-->
            <div class="grid grid-cols-[minmax(280px,_1fr)] row-span-1" @mouseover="onHoverSubject"
                 @mouseleave="onLeaveSubject">
                <span :id="emailItem.id + '-subject'"
                      class="text-ellipsis overflow-hidden whitespace-nowrap font-bold self-center">
                    {{emailItem.subject || '[No Subject]'}}
                </span>
                <div :class="subjectHoverHidden +' bg-black p-1 rounded-md shadow-md absolute font-bold'">
                    {{emailItem.subject}}
                </div>
            </div>

            <!--Item Date-->
            <div class="grid row-span-2 self-start text-center text-xs font-medium">
                <span>{{emailFormattedDate}}</span>
            </div>

            <!--Item Body-->
            <div class="grid row-span-1 grid-cols-[minmax(280px,_1fr)]">
                <p class="text-ellipsis overflow-hidden whitespace-nowrap self-center" v-html="bodyHighlight"></p>
            </div>
        </div>
    </div>
    <div v-else>
        <div class="grid grid-cols-[100px_1fr_100px] rounded-xl bg-gradient-to-r from-sky-500
        to-indigo-500 text-white"
             @click="onClickItem">

            <!--Item Icon-->
            <div class="grid items-center justify-center row-span-3 h-16 w-16 rounded-full text-3xl
            text-center bg-violet-800 self-center justify-self-center">
                <span class="text-white">
                    {{emailItem.from.charAt(0).toUpperCase()}}
                </span>
            </div>

            <!--Item Subject-->
            <div class="grid grid-cols-[minmax(280px,_1fr)] h-6">
                <span class="text-ellipsis overflow-hidden whitespace-nowrap font-bold">
                    {{emailItem.subject || '[No Subject]'}}
                </span>
            </div>

            <!--Item Date-->
            <div class="grid row-span-3 self-start text-center text-xs font-medium">
                <span>{{emailFormattedDate}}</span>
            </div>

            <!--Item From-->
            <div class="h-6">
                <span><strong>From:</strong> {{emailItem.from}}</span>
            </div>

            <!--Item To-->
            <div class="h-6">
                <span><strong>To:</strong> {{emailItem.to}}</span>
            </div>

            <!--Item Body-->
            <div class="grid auto-rows-auto col-span-3 px-5 m-4">
                <p class="text-justify whitespace-pre-line" v-html="bodyHighlight"></p>
            </div>
        </div>
    </div>
</template>

<script>
  export default {
    name: "EmailItem",
    props: {
      emailItem: Object,
      term: String
    },
    components: {},
    methods: {
      onClickItem() {
        this.itemCollapsed = !this.itemCollapsed
      },
      onHoverSubject() {
        const truncateText = document.getElementById(this.emailItem.id + '-subject');
        const truncateTextWidth = truncateText.offsetWidth;
        const truncateTextContentWidth = (truncateText.textContent.length * 8);

        if (truncateTextWidth < truncateTextContentWidth) {
          this.subjectHoverHidden = "";
        } else {
          this.subjectHoverHidden = "hidden";
        }
      },
      onLeaveSubject() {
        this.subjectHoverHidden = 'hidden';
      }
    },
    data() {
      return {
        itemCollapsed: true,
        subjectHoverHidden: "hidden"
      }
    },
    computed: {
      emailFormattedDate() {
        const date = new Date(this.emailItem.date);
        return date.toLocaleDateString("en-US", {
          year: "numeric",
          month: "2-digit",
          day: "2-digit"
        });
      },
      bodyHighlight() {
        let content = this.emailItem.body;
        let index = content.toLowerCase().indexOf(this.term.toLowerCase());

        if (index >= 0) {
          content = content.split('');
          content.splice(
            index,
            this.term.length,
            '<span class="bg-slate-900">' + content.slice(index, index + this.term.length).join('') + '</span>');
          content = content.join('');
        }

        return content;
      }
    }
  }
</script>

<style scoped>

</style>