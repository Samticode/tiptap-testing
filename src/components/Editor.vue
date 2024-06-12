<script setup lang="ts">
import * as Y from "yjs";
import { useEditor, EditorContent } from '@tiptap/vue-3'
import StarterKit from '@tiptap/starter-kit'
import { WebrtcProvider } from 'y-webrtc'
import Collaboration from "@tiptap/extension-collaboration";
import CollaborationCursor from "@tiptap/extension-collaboration-cursor";
import Emoji, { gitHubEmojis } from '@tiptap-pro/extension-emoji'

const ydoc = new Y.Doc();
const provider = new WebrtcProvider("example-document", ydoc);

const editor = useEditor({
    extensions: [
        StarterKit,
        Collaboration.configure({
            document: ydoc,
        }),
        CollaborationCursor.configure({
            provider: provider,
            user: {
                name: "Samti",
                color: "#FF5630",
            },
        }),
        Emoji.configure({
            emojis: gitHubEmojis,
            enableEmoticons: true,
        }),
    ],
    content: '',
})

const emojis = ['😀', '😃', '😄', '😁', '😆', '😅', '😂', '🤣', '😊', '😇', '🙂', '🙃', '😉', '😌', '😍'];

const setEmoji = (emoji) => {
    editor.value?.chain().focus().insertContent(emoji).run();
}


</script>

<template>
    <EditorContent :editor="editor" />
    <div class="emoji-selector-container" >
        <div v-for="(emoji, index) in emojis" :key="index" @click="setEmoji(emoji)">{{ emoji }}</div>
    </div>
</template>

<style>
.ProseMirror {
  width: 100%;
  background-color: var(--white);
  color: var(--black);
  padding: 10px 20px;

  img {
    height: 20px;
    width: 20px;
  }
}

.collaboration-cursor__caret {
  border-left: 1px solid #0d0d0d;
  border-right: 1px solid #0d0d0d;
  margin-left: -1px;
  margin-right: -1px;
  pointer-events: none;
  position: relative;
  word-break: normal;
}

/* Render the username above the caret */
.collaboration-cursor__label {
  border-radius: 3px 3px 3px 0;
  color: #0d0d0d;
  font-size: 12px;
  font-style: normal;
  font-weight: 600;
  left: -1px;
  line-height: normal;
  padding: 0.1rem 0.3rem;
  position: absolute;
  top: -1.4em;
  user-select: none;
  white-space: nowrap;
}
.emoji-selector-container {
    width: 100%;
    height: 75%;
    background-color: var(--white);
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    place-items: center;

    div {
        font-size: 2rem;
        cursor: pointer;
    }
}
</style>