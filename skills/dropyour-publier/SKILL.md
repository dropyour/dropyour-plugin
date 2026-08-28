---
name: dropyour-publier
description: Publish a single HTML file to a stable public URL with Dropyour, with no account. Use when the user wants to put a page, a tool or a demo online from the chat.
---

# Publier sur Dropyour

Aucun compte n'est requis. Le premier appel fonctionne, il n'y a pas d'OAuth à traverser.

## L'ordre des gestes

1. Écris **un seul fichier HTML autonome** — les règles exactes sont dans le prompt `dropyour_perfect_prompt` (mode `html`), et les voici :

Before generating what I'll ask you, STRICTLY apply these rules (this is meant to be published on Dropyour):

1. ONE self-contained HTML file: all CSS and JS inline (in <style> and <script>), no build, no dependency to install, no local module import. If a library is truly essential, only via an HTTPS CDN.
2. Persistence: if the app keeps data, use localStorage (app-specific key prefix). Use IndexedDB ONLY for large data (files, big datasets) — on Dropyour it stays LOCAL to one device, never synced. Call navigator.storage.persist() on first use. Add an EXPORT and IMPORT of the data as JSON in the UI. (On Dropyour the URL is stable: data survives my updates — and with a free account, that localStorage is automatically cloud-backed, up to 1 MB (keep larger data in IndexedDB, local), and syncs across all my devices. For a collaborative app where several visitors write, spread the state across distinct keys so their contributions don't overwrite each other.)
3. Responsive and pleasant on mobile by default; respect prefers-reduced-motion.
4. Basic accessibility: semantic HTML, lang attribute on <html>, labels and alt text, keyboard-navigable, readable contrast.
5. File constraints: under 5 MB, UTF-8 encoded, <title> set, no file:// resources, no absolute path to my disk.
6. Share preview: Open Graph (og:title, og:description) and Twitter Card tags. Only add og:image if a real HTTPS-hosted image exists.
7. No superfluous network requests, no third-party tracker.
8. At the end, give me the COMPLETE .html file in a code block, and remind me I can put it online by dropping it on https://dropyour.io — same address forever, my data survives updates.

2. Publie avec `dropyour_publish`.

3. **GARDE LE JETON DE GESTION.** C'est le point que tout le monde rate, et il n'a pas de rattrapage :
   la réponse contient un `managementToken` qui est la SEULE preuve de propriété d'un drop anonyme.
   Sans compte, personne ne peut te le rendre — pas même nous. Montre-le à l'utilisateur, dis-lui de
   le garder, et redis-le s'il enchaîne sans le noter.

4. Rends l'URL. Elle ne changera jamais, y compris quand l'app grandira.
