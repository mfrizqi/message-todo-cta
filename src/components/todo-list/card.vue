<script setup>
import "cally";
</script>
<template>
  <section
    class="w-full flex gap-4 border-b border-gray-900 text-sm pb-5"
  >
    <div>
      <input
        type="checkbox"
        defaultChecked
        class="checkbox text-gray-500 rounded-sm h-[20px] w-[20px] border-2 border-gray-500 checked:shadow-none mt-1"
      />
    </div>
    <div class="flex flex-col gap-6 grow">
      <div class="flex justify-between">
        <div class="text-gray-700 font-semibold text-wrap shrink w-xs">
          Set up documentation report for several Cases : Case 145443, Case
          192829 and Case 182203
        </div>
        <div class="flex gap-2">
          <!-- <div>expired</div> -->
          <div class="text-[#EB5757] shrink-0">2 days left</div>
          <div class="text-gray-700 shrink-0">12/06/21</div>
          <img
            src="../../assets/img/icon/chevron-up.svg"
            class="h-[16px] w-[16px] shrink-0"
          />
          <div>
            <img
              src="../../assets/img/icon/more-horizontal.svg"
              class="h-[16px] w-[16px] shrink-0"
            />
          </div>
        </div>
      </div>
      <div class="flex gap-3 text-gray-700 items-center">
        <img src="../../assets/img/icon/clock.svg" class="h-[20px] w-[20px]" />
        <div>
          <button
            popovertarget="cally-popover1"
            class="input input-border bg-white border border-gray-500 rounded w-[194px] flex justify-between"
            style="anchor-name: --cally1"
          >
            <span id="cally1">Set date</span> <img src="../../assets/img/icon/calendar.svg" class="w-[16px] h-[16px]">
          </button>
          <div
            popover
            id="cally-popover1"
            class="dropdown bg-white rounded-md border border-gray-500 shadow-lg mt-1"
            style="position-anchor: --cally1"
          >
            <calendar-date
              class="cally"
              onchange="document.getElementById('cally1').innerText = this.value"
            >
              <svg
                aria-label="Previous"
                class="fill-gray-500 size-4 hover:bg-transparent"
                slot="previous"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
              >
                <path d="M15.75 19.5 8.25 12l7.5-7.5"></path>
              </svg>
              <svg
                aria-label="Next"
                class="fill-gray-500 size-4"
                slot="next"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
              >
                <path d="m8.25 4.5 7.5 7.5-7.5 7.5"></path>
              </svg>
              <calendar-month></calendar-month>
            </calendar-date>
          </div>
        </div>
      </div>
      <div class="flex gap-3 text-gray-700">
        <img src="../../assets/img/icon/pen.svg" class="h-[15px] w-[15px] mt-1" />
        <div class="w-lg">
          Closing off this case since this application has been cancelled. No
          one really understand how this case could possibly be cancelled. The
          options and the documents within this document were totally a
          guaranteed for a success!
        </div>
      </div>
    </div>
  </section>
</template>

<style></style>
