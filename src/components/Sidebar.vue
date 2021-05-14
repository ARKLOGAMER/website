<template>
	<div class="hidden relative lg:flex lg:flex-shrink-0 navbar-color">
		<div class="flex flex-col w-64 z-10">
			<div class="flex flex-col h-0 flex-1">
				<div class="flex-1 flex flex-col pb-4">
					<nav class="mt-5 flex-1 px-2 space-y-1">
						<ul>
							<li v-for="(category, categoryId) in docs?.custom" :key="categoryId">
								<Disclosure v-slot="{ open }" :default-open="true">
									<DisclosureButton class="focus:outline-none" tabindex="-1">
										<div
											class="text-gray-800 dark:text-gray-100 py-2 text-md font-bold uppercase flex gap-1 items-center"
										>
											<button
												class="
													leading-3
													rounded-md
													p-1
													focus:outline-none
													focus-visible:ring-1 focus-visible:ring-white
												"
												:aria-expanded="open"
											>
												<span class="sr-only">{{ open ? 'Shrink' : 'Expand' }}</span>
												<heroicons-outline-chevron-right
													class="inline-block"
													:class="{ hidden: open }"
													aria-hidden="true"
												/>
												<heroicons-outline-chevron-down
													class="inline-block"
													:class="{ hidden: !open }"
													aria-hidden="true"
												/>
											</button>
											{{ category.name }}
										</div>
									</DisclosureButton>
									<DisclosurePanel as="ul">
										<li v-for="(file, fileId) in category.files" :key="fileId">
											<router-link
												:to="{
													name: 'docs-source-tag-category-file',
													params: { source: source?.id, tag: tag, category: categoryId, file: fileId },
												}"
												class="
													text-gray-600
													dark:text-gray-300
													border-l-4 border-transparent
													rounded-sm
													hover:border-l-4 hover:border-discord-blurple-500
													hover:text-gray-800
													dark:hover:text-gray-100
													group
													flex
													items-center
													px-3
													py-2
													text-sm
													font-semibold
													focus:outline-none
													focus-visible:ring-1 focus-visible:ring-white
												"
												exact-active-class="border-l-4 border-discord-blurple-530 text-gray-900"
											>
												{{ typeof file === 'object' ? file.name : file }}
											</router-link>
										</li>
									</DisclosurePanel>
								</Disclosure>
							</li>

							<Disclosure v-slot="{ open }" as="li" :default-open="true">
								<DisclosureButton class="focus:outline-none" tabindex="-1">
									<div
										class="text-gray-800 dark:text-gray-100 py-2 text-md font-bold uppercase flex gap-1 items-center"
									>
										<button
											class="leading-3 rounded-md p-1 focus:outline-none focus-visible:ring-1 focus-visible:ring-white"
											:aria-expanded="open"
										>
											<span class="sr-only">{{ open ? 'Shrink' : 'Expand' }}</span>
											<heroicons-outline-chevron-right
												class="inline-block"
												:class="{ hidden: open }"
												aria-hidden="true"
											/>
											<heroicons-outline-chevron-down
												class="inline-block"
												:class="{ hidden: !open }"
												aria-hidden="true"
											/>
										</button>
										Classes
									</div>
								</DisclosureButton>
								<DisclosurePanel as="ul">
									<li v-for="cls in docs?.classes" :key="cls.name">
										<router-link
											exact
											:to="{
												name: 'docs-source-tag-class-class',
												params: { source: source?.id, tag: tag, class: cls.name },
											}"
											class="
												text-gray-600
												dark:text-gray-300
												border-l-4 border-transparent
												rounded-sm
												hover:border-l-4 hover:border-discord-blurple-500
												hover:text-gray-800
												dark:hover:text-gray-100
												group
												flex
												items-center
												px-3
												py-2
												text-sm
												font-semibold
												focus:outline-none
												focus-visible:ring-1 focus-visible:ring-white
											"
											exact-active-class="border-l-4 border-discord-blurple-530 text-gray-900"
										>
											{{ cls.name }}
										</router-link>
									</li>
								</DisclosurePanel>
							</Disclosure>

							<Disclosure v-slot="{ open }" as="li" :default-open="true">
								<DisclosureButton class="focus:outline-none" tabindex="-1">
									<div
										class="text-gray-800 dark:text-gray-100 py-2 text-md font-bold uppercase flex gap-1 items-center"
									>
										<button
											class="leading-3 rounded-md p-1 focus:outline-none focus-visible:ring-1 focus-visible:ring-white"
											:aria-expanded="open"
										>
											<span class="sr-only">{{ open ? 'Shrink' : 'Expand' }}</span>
											<heroicons-outline-chevron-right
												class="inline-block"
												:class="{ hidden: open }"
												aria-hidden="true"
											/>
											<heroicons-outline-chevron-down
												class="inline-block"
												:class="{ hidden: !open }"
												aria-hidden="true"
											/>
										</button>
										Typedefs
									</div>
								</DisclosureButton>
								<DisclosurePanel as="ul">
									<li v-for="typedef in docs?.typedefs" :key="typedef.name">
										<router-link
											exact
											:to="{
												name: 'docs-source-tag-typedef-typedef',
												params: { source: source?.id, tag: tag, typedef: typedef.name },
											}"
											class="
												text-gray-600
												dark:text-gray-300
												border-l-4 border-transparent
												rounded-sm
												hover:border-l-4 hover:border-discord-blurple-500
												hover:text-gray-800
												dark:hover:text-gray-100
												group
												flex
												items-center
												px-3
												py-2
												text-sm
												font-semibold
												focus:outline-none
												focus-visible:ring-1 focus-visible:ring-white
											"
											exact-active-class="border-l-4 border-discord-blurple-530 text-gray-900"
										>
											{{ typedef.name }}
										</router-link>
									</li>
								</DisclosurePanel>
							</Disclosure>
						</ul>
					</nav>
				</div>
			</div>
		</div>
		<div class="overkill-border"></div>
	</div>
</template>

<script setup lang="ts">
import { computed } from 'vue';

import { useStore } from '~/store';

import { Disclosure, DisclosureButton, DisclosurePanel } from '@headlessui/vue';

const store = useStore();

const source = computed(() => store.state.source);
const tag = computed(() => store.state.tag);
const docs = computed(() => store.state.docs);
</script>

<style>
.overkill-border {
	left: calc(100% + 2px);
	right: auto;
	pointer-events: none;
	position: absolute;
	top: 0;
	bottom: 0;
	z-index: 6;
}

.overkill-border::before {
	content: '';
	position: absolute;
	top: 0;
	right: 0;
	bottom: 0;
	background: linear-gradient(90deg, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.07));
	width: 5px;
	opacity: 0.8;
}

.dark .overkill-border::before {
	content: '';
	position: absolute;
	top: 0;
	right: 0;
	bottom: 0;
	background: rgb(0, 0, 0);
	border-right: 1px solid rgba(255, 255, 255, 0.15);
	width: 1px;
	opacity: 1;
}

.overkill-border::after {
	content: '';
	position: absolute;
	top: 0;
	bottom: 0;
	background: linear-gradient(90deg, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.07));
	opacity: 1;
	width: 2px;
	opacity: 0.5;
}

.dark .overkill-border::after {
	content: '';
	position: absolute;
	top: 0;
	bottom: 0;
	background: linear-gradient(90deg, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.07));
	opacity: 1;
	width: 14px;
	right: 1px;
}

.dark .navbar-color::before {
	content: '';
	position: absolute;
	top: 0;
	right: 0;
	bottom: 0;
	width: 999em;
	background: #191919;
	pointer-events: none;
}
</style>
