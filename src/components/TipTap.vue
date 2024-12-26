<script setup>
import Image from './DropImage';

import {EditorContent, useEditor,} from '@tiptap/vue-3';
import StarterKit from '@tiptap/starter-kit';
import Underline from '@tiptap/extension-underline';
import Link from '@tiptap/extension-link'; //https://tiptap.dev/docs/editor/extensions/marks/link config what u need
import Table from '@tiptap/extension-table';
import TableCell from '@tiptap/extension-table-cell';
import TableHeader from '@tiptap/extension-table-header';
import TableRow from '@tiptap/extension-table-row';
import TextAlign from '@tiptap/extension-text-align';


import SvgIcon from '@jamescoyle/vue-icon';
import {
	mdiFormatAlignCenter,
	mdiFormatAlignJustify,
	mdiFormatAlignLeft,
	mdiFormatAlignRight,
	mdiFormatBold,
	mdiFormatClear,
	mdiFormatHeader1,
	mdiFormatHeader2,
	mdiFormatHeader3,
	mdiFormatItalic,
	mdiFormatListBulleted,
	mdiFormatListNumbered,
	mdiFormatParagraph,
	mdiFormatQuoteClose,
	mdiFormatUnderline,
	mdiMinus,
	mdiRedo,
	mdiUndo
} from '@mdi/js';


const editor = useEditor({
	extensions: [StarterKit, Underline, Link, Table.configure({resizable: true}), TableCell, Image, TableHeader, TableRow,
		TextAlign.configure({
			types: ['heading', 'paragraph'],
		})],
	content: `<h1>Заголовок 2</h1><h2>Заголовок 2</h2><h3>Заголовок 2</h3><p>С другой <strong>стороны </strong>сложившаяся <u>структура организации позволяет выполнять важные</u> задания по разработке системы обучения кадров, соответствует насущным потребностям. Повседневная практика показывает, что постоянный количественный р<em>ост и сфера нашей активности</em> требуют определения и уточнения систем массового участия. С другой стороны новая модель организационной деятельности обеспечивает широкому кругу (специалистов) участие в формировании систем массового участия.</p><p><br class="ProseMirror-trailingBreak"></p><p><strong>жирный</strong></p><p><u>подчеркивание</u></p><p><em>кривой</em></p><p><strong><em><u>все в одном</u></em></strong></p><p><br class="ProseMirror-trailingBreak"></p><ul><li><p>список</p></li><li><p>без нумерции</p></li></ul><p><br class="ProseMirror-trailingBreak"></p><ol><li><p>Список </p></li><li><p>с нунирацией</p></li></ol><p><br class="ProseMirror-trailingBreak"></p><blockquote><p>Задача организации, в особенности же дальнейшее развитие различных форм деятельности позволяет выполнять важные задания по разработке дальнейших направлений развития. Таким образом начало повседневной работы по формированию позиции играет важную роль в формировании систем массового участия. Не следует, однако забывать, что реализация намеченных плановых заданий позволяет выполнять важные задания по разработке модели развития. Таким образом реализация намеченных плановых заданий требуют определения и уточнения модели развития. Идейные соображения высшего порядка, а также постоянное информационно-пропагандистское обеспечение нашей деятельности требуют от нас анализа позиций, занимаемых участниками в отношении поставленных задач.</p></blockquote><p>Try to <b>scroll</b> inside this frame to understand how sticky positioning works.</p>
		<p> Note: IE/ Edge 15 and earlier versions do not support sticky position.</p>

<div class="sticky">I am sticky!</div>

<div style="padding-bottom:2000px">
  <p>In this example, the sticky element sticks to the top of the page (top: 0), when you reach its scroll position.</p>
  <p>Some text to enable scrolling.. Lorem ipsum dolor sit amet, illum definitiones no quo, maluisset concludaturque et eum, altera fabulas ut quo. Atqui causae gloriatur ius te, id agam omnis evertitur eum. Affert laboramus repudiandae nec et. Inciderint efficiantur his ad. Eum no molestiae voluptatibus.</p>
  <p>Some text to enable scrolling.. Lorem ipsum dolor sit amet, illum definitiones no quo, maluisset concludaturque et eum, altera fabulas ut quo. Atqui causae gloriatur ius te, id agam omnis evertitur eum. Affert laboramus repudiandae nec et. Inciderint efficiantur his ad. Eum no molestiae voluptatibus.</p>
</div> <p>Try to <b>scroll</b> inside this frame to understand how sticky positioning works.</p>
<p>Note: IE/Edge 15 and earlier versions do not support sticky position.</p>

<div class="sticky">I am sticky!</div>

<div style="padding-bottom:2000px">
  <p>In this example, the sticky element sticks to the top of the page (top: 0), when you reach its scroll position.</p>
  <p>Some text to enable scrolling.. Lorem ipsum dolor sit amet, illum definitiones no quo, maluisset concludaturque et eum, altera fabulas ut quo. Atqui causae gloriatur ius te, id agam omnis evertitur eum. Affert laboramus repudiandae nec et. Inciderint efficiantur his ad. Eum no molestiae voluptatibus.</p>
  <p>Some text to enable scrolling.. Lorem ipsum dolor sit amet, illum definitiones no quo, maluisset concludaturque et eum, altera fabulas ut quo. Atqui causae gloriatur ius te, id agam omnis evertitur eum. Affert laboramus repudiandae nec et. Inciderint efficiantur his ad. Eum no molestiae voluptatibus.</p>
</div>`,
	editorProps: {
		attributes: {
			class: 'editor',
		},
		transformPastedText(text) {
			return text.toUpperCase()
		}
	},
	onUpdate: ({editor}) => {
		console.log(editor.getHTML());
	}
})


const setLink = () => {
	const previousUrl = editor.value.getAttributes('link').href
	const url = window.prompt('URL', previousUrl)

	// cancelled
	if (url === null) {
		return
	}

	// empty
	if (url === '') {
		editor.value
			.chain()
			.focus()
			.extendMarkRange('link')
			.unsetLink()
			.run()

		return
	}

	// update link
	editor.value
		.chain()
		.focus()
		.extendMarkRange('link')
		.setLink({href: url})
		.run()
}

</script>


<template>
	<div class="tiptap__editor">
		<div class="toolbar" v-if="editor">
			<div>
				<button @click="editor.chain().focus().toggleBold().run()" :disabled="!editor.can().chain().focus().toggleBold().run()" :class="{ 'is-active': editor.isActive('bold') }" title="Полужирный (Ctrl+B)">
					<svg-icon type="mdi" :path="mdiFormatBold" :size="26"/>
				</button>
				<button @click="editor.chain().focus().toggleItalic().run()" :disabled="!editor.can().chain().focus().toggleItalic().run()" :class="{ 'is-active': editor.isActive('italic') }" title="Курсив (Ctrl+I)">
					<svg-icon type="mdi" :path="mdiFormatItalic" :size="26"/>
				</button>
				<button @click="editor.chain().focus().toggleUnderline().run()" :disabled="!editor.can().chain().focus().toggleUnderline().run()" :class="{ 'is-active': editor.isActive('underline') }" title="Подчеркнутый (Ctrl+U)">
					<svg-icon type="mdi" :path="mdiFormatUnderline" :size="26"/>
				</button>
			</div>
			<div>
				<button @click="editor.chain().focus().setParagraph().run()" :class="{ 'is-active': editor.isActive('paragraph') }" title="Обычный текст (Ctrl+Alt+0)">
					<svg-icon type="mdi" :path="mdiFormatParagraph" :size="26"/>
				</button>
				<button @click="editor.chain().focus().toggleHeading({ level: 1 }).run()" :class="{ 'is-active': editor.isActive('heading', { level: 1 }) }" title="Заголовок 1 (Ctrl+Alt+1)">
					<svg-icon type="mdi" :path="mdiFormatHeader1" :size="26"/>
				</button>
				<button @click="editor.chain().focus().toggleHeading({ level: 2 }).run()" :class="{ 'is-active': editor.isActive('heading', { level: 2 }) }" title="Заголовок 2 (Ctrl+Alt+2)">
					<svg-icon type="mdi" :path="mdiFormatHeader2" :size="26"/>
				</button>
				<button @click="editor.chain().focus().toggleHeading({ level: 3 }).run()" :class="{ 'is-active': editor.isActive('heading', { level: 3 }) }" title="Заголовок 3 (Ctrl+Alt+3)">
					<svg-icon type="mdi" :path="mdiFormatHeader3" :size="26"/>
				</button>
			</div>
			<div>
				<button @click="editor.chain().focus().toggleBulletList().run()" :class="{ 'is-active': editor.isActive('bulletList') }" title="Маркированный список (Ctrl+Shift+8)">
					<svg-icon type="mdi" :path="mdiFormatListBulleted" :size="26"/>
				</button>
				<button @click="editor.chain().focus().toggleOrderedList().run()" :class="{ 'is-active': editor.isActive('orderedList') }" title="Упорядоченный список (Ctrl+Shift+7)">
					<svg-icon type="mdi" :path="mdiFormatListNumbered" :size="26"/>
				</button>
			</div>
			<div>
				<button @click="editor.chain().focus().toggleBlockquote().run()" :class="{ 'is-active': editor.isActive('blockquote') }" title="Цитата (Ctrl+Shift+B)">
					<svg-icon type="mdi" :path="mdiFormatQuoteClose" :size="26"/>
				</button>
				<button @click="editor.chain().focus().clearNodes().run()" title="Очистка форматирования">
					<svg-icon type="mdi" :path="mdiFormatClear" :size="26"/>
				</button>
				<button @click="editor.chain().focus().setHorizontalRule().run()" title="Горизонтальное линия">
					<svg-icon type="mdi" :path="mdiMinus" :size="26"/>
				</button>
			</div>
			<div>
				<button @click="editor.chain().focus().undo().run()" :disabled="!editor.can().chain().focus().undo().run()" title="Отменить изменения (Ctrl+Z)">
					<svg-icon type="mdi" :path="mdiUndo" :size="26"/>
				</button>
				<button @click="editor.chain().focus().redo().run()" :disabled="!editor.can().chain().focus().redo().run()" title="Вернуть изменения (Ctrl+Shift+Z)">
					<svg-icon type="mdi" :path="mdiRedo" :size="26"/>
				</button>
			</div>
			<div>
				<button @click="setLink" :class="{ 'is-active': editor.isActive('link') }">
					Set link
				</button>
				<button @click="editor.chain().focus().unsetLink().run()" :disabled="!editor.isActive('link')">
					Unset link
				</button>
			</div>
			<div>
				<button @click="editor.chain().focus().setTextAlign('left').run()" :class="{ 'is-active': editor.isActive({ textAlign: 'left' }) }" title="Выравнивание по левому краю (Ctrl+Shift+L)">
					<svg-icon type="mdi" :path="mdiFormatAlignLeft" :size="24"/>
				</button>
				<button @click="editor.chain().focus().setTextAlign('center').run()" :class="{ 'is-active': editor.isActive({ textAlign: 'center' }) }" title="Выравнивание по центру (Ctrl+Shift+E)">
					<svg-icon type="mdi" :path="mdiFormatAlignCenter" :size="24"/>
				</button>
				<button @click="editor.chain().focus().setTextAlign('right').run()" :class="{ 'is-active': editor.isActive({ textAlign: 'right' }) }" title="Выравнивание по правому краю (Ctrl+Shift+R)">
					<svg-icon type="mdi" :path="mdiFormatAlignRight" :size="24"/>
				</button>
				<button @click="editor.chain().focus().setTextAlign('justify').run()" :class="{ 'is-active': editor.isActive({ textAlign: 'justify' }) }" title="Выравнивание по ширине (Ctrl+Shift+J)">
					<svg-icon type="mdi" :path="mdiFormatAlignJustify" :size="24"/>
				</button>
			</div>
			<div v-if="false">
				<button @click="editor.chain().focus().insertTable({ rows: 3, cols: 3, withHeaderRow: true }).run()">
					insertTable
				</button>
				<button @click="editor.chain().focus().addColumnBefore().run()" :disabled="!editor.can().addColumnBefore()">
					addColumnBefore
				</button>
				<button @click="editor.chain().focus().addColumnAfter().run()" :disabled="!editor.can().addColumnAfter()">
					addColumnAfter
				</button>
				<button @click="editor.chain().focus().deleteColumn().run()" :disabled="!editor.can().deleteColumn()">
					deleteColumn
				</button>
				<button @click="editor.chain().focus().addRowBefore().run()" :disabled="!editor.can().addRowBefore()">
					addRowBefore
				</button>
				<button @click="editor.chain().focus().addRowAfter().run()" :disabled="!editor.can().addRowAfter()">
					addRowAfter
				</button>
				<button @click="editor.chain().focus().deleteRow().run()" :disabled="!editor.can().deleteRow()">
					deleteRow
				</button>
				<button @click="editor.chain().focus().deleteTable().run()" :disabled="!editor.can().deleteTable()">
					deleteTable
				</button>
				<button @click="editor.chain().focus().mergeCells().run()" :disabled="!editor.can().mergeCells()">
					mergeCells
				</button>
				<button @click="editor.chain().focus().splitCell().run()" :disabled="!editor.can().splitCell()">
					splitCell
				</button>
				<button @click="editor.chain().focus().toggleHeaderColumn().run()" :disabled="!editor.can().toggleHeaderColumn()">
					toggleHeaderColumn
				</button>
				<button @click="editor.chain().focus().toggleHeaderRow().run()" :disabled="!editor.can().toggleHeaderRow()">
					toggleHeaderRow
				</button>
				<button @click="editor.chain().focus().toggleHeaderCell().run()" :disabled="!editor.can().toggleHeaderCell()">
					toggleHeaderCell
				</button>
				<button @click="editor.chain().focus().mergeOrSplit().run()" :disabled="!editor.can().mergeOrSplit()">
					mergeOrSplit
				</button>
				<button @click="editor.chain().focus().setCellAttribute('backgroundColor', '#FAF594').run()" :disabled="!editor.can().setCellAttribute('backgroundColor', '#FAF594')">
					setCellAttribute
				</button>
				<button @click="editor.chain().focus().fixTables().run()" :disabled="!editor.can().fixTables()">
					fixTables
				</button>
				<button @click="editor.chain().focus().goToNextCell().run()" :disabled="!editor.can().goToNextCell()">
					goToNextCell
				</button>
				<button @click="editor.chain().focus().goToPreviousCell().run()" :disabled="!editor.can().goToPreviousCell()">
					goToPreviousCell
				</button>
			</div>
		</div>
		<div class="create__post">
			<input class='tiptap__input' type="text" placeholder="Заголовок статьи">
			<div class="editor__wrapper">
				<editor-content :editor="editor"/>
			</div>
		</div>
	</div>
</template>

<style>
.tiptap table {
	border-collapse: collapse;
	table-layout: fixed;
	width: 100%;
	margin: 0;
	overflow: hidden;
}

.tiptap table td,
.tiptap table th {
	min-width: 1em;
	border: 2px solid #ced4da;
	padding: 3px 5px;
	vertical-align: top;
	box-sizing: border-box;
	position: relative;
}

.tiptap table td > *,
.tiptap table th > * {
	margin-bottom: 0;
}

.tiptap table th {
	font-weight: bold;
	text-align: left;
	background-color: #f1f3f5;
}

.tiptap table .selectedCell:after {
	z-index: 2;
	position: absolute;
	content: "";
	left: 0;
	right: 0;
	top: 0;
	bottom: 0;
	background: rgba(200, 200, 255, 0.4);
	pointer-events: none;
}

.tiptap table .column-resize-handle {
	position: absolute;
	right: -2px;
	top: 0;
	bottom: -2px;
	width: 4px;
	background-color: #adf;
	pointer-events: none;
}

.tiptap table p {
	margin: 0;
}

.tableWrapper {
	padding: 1rem 0;
	overflow-x: auto;
}

.resize-cursor {
	cursor: ew-resize;
	cursor: col-resize;
}

.tiptap__editor {
	height: 100%;
	max-width: 1240px;
	margin: 0 auto;

}

.editor {
	padding: 4px;
	width: 100%;
	outline: none;
	margin: 0;
	height: 100%;

}

.editor__wrapper {
	height: calc(100% - 60px);
}

.editor__wrapper > div {
	height: 100%;
}

.toolbar {
	width: 100%;
	border-bottom: 1px solid rgb(206, 201, 201);

	background-color: white;

	position: -webkit-sticky;
	position: sticky;
	top: 0;
	z-index: 5;

}

.toolbar.unfocused {
	opacity: 0.2;
	pointer-events: none;
}

.tiptap__input {
	outline: none;
	width: 100%;
	height: 60px;
	font-size: 30px;
	font-weight: bold;
	color: inherit;
	border: none;
}

.create__post {
	margin-left: 60px;
	height: calc(100% - 50px);
	max-width: 700px;
	margin: 0 auto;
}

.toolbar {
	height: 50px;
	display: flex;
	flex-direction: row;
	align-items: center;
}

.toolbar > div {
	display: flex;
}

.toolbar > div:not(:first-child) {

	border-left: 1px solid rgb(206, 201, 201);
}

.toolbar button {
	background-color: transparent;
	border: none;
	cursor: pointer;
	color: rgb(52, 69, 99);
	border-radius: 2px;

	display: flex;
	justify-content: center;
	align-items: center;
	margin: 0 1px;
}

.toolbar button:disabled {
	opacity: 0.2;
}

.toolbar button:hover {
	background: rgb(206, 201, 201);
}

.toolbar button.is-active {
	color: white;
	background: rgb(52, 69, 99);
}

.editor blockquote {
	border-left: 3px solid rgb(52, 69, 99);
	padding: 2px 10px;
}
</style>
