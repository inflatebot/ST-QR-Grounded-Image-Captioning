# ST-QR-Grounded-Image-Captioning

Unfortunately, multimodal models haven't taken over the world yet. Most of the roleplay models we use are still text-only. SillyTavern's built-in Image Captioning extension is a cool way of emulating multimodal functionality; but it's a little unwieldy. The extension doesn't have any way of sending the context of the ongoing chat in the caption prompt, and the caption prompt doesn't expand macros.

But with the power of Quick Replies and STscript, we can get *altogether pretty close* to a true multimodal experience, with inline messages, *without* having to use a Chat Completions API and a model whose writing we might not otherwise like (or having to rack up the expenses that come with sending sometimes *multiple* inline images to a CC API with every swipe! Ask me how I spent $5 of OpenRouter credit in a single play session one day!)

GIC collects the chat history, character, and persona information, and builds a "micro-prompt" that gives the image captioning model the information it'll need to make more accurate, coherent and relevant captions for your images.

To simply use GIC as a manual Quick Reply, you don't need any extensions, but if you want to automatically caption images as they're sent, then you'll need [SillyTavern-GetContext](https://github.com/LenAnderson/SillyTavern-GetContext).

Known limitations:

- I am unaware of any way to attach the caption to the image directly in STscript, without also sending a duplicate image. So rather than do it the normal way, GIC simply inserts the caption as a system message at depth 0.
- The "verify caption" dialogue had to be recreated with a popup, but I have no easy way to send the caption back or redo it for the moment.
- (The above two points could be ameliorated by simply deleting the message and effectively replacing it with the captioned one, but that feels like it would break pretty easily, and that is not fail-safe behavior...)
- Generating history takes a little bit.
