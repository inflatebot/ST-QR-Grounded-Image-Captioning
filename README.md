# ST-QR-Grounded-Image-Captioning

Unfortunately, multimodal models haven't taken over the world yet. Most of the roleplay models we use are still text-only. SillyTavern's built-in Image Captioning extension is a cool way of emulating multimodal functionality; but it's a little unwieldy. The extension doesn't have any way of sending the context of the ongoing chat in the caption prompt, and the caption prompt doesn't expand macros.

But with the power of Quick Replies and STscript, we can get *altogether pretty close* to a true multimodal experience, with inline messages, *without* having to use a Chat Completions API and a model whose writing we might not otherwise like (or having to rack up the expenses that come with sending sometimes *multiple* inline images to a CC API with every swipe! Ask me how I spent $5 of OpenRouter credit in a single play session one day!)

GIC collects the chat history, character, and persona information, and builds a "micro-prompt" that gives the image captioning model the information it'll need to make more accurate, coherent and relevant captions for your images.

To simply use GIC as a manual Quick Reply, you don't need any extensions, but if you want to automatically caption images as they're sent, then you'll need [SillyTavern-GetContext](https://github.com/LenAnderson/SillyTavern-GetContext).

Usage:
- Optional: Install GetContext.
- Download "Grounded-Image-Captioning.json"
- In the Extensions Menu, open the Quick Reply section, and under Edit Quick Replies, click "Import quick reply set". (It's the one that has an arrow pointing into a piece of paper.)
- Under Global Quick Reply Sets, click the plus icon.
- In the dropdown, select "Grounded-Image-Captioning" and enable "Buttons".
- Make sure a Multimodal source is configured under "Image Captioning."
- Also under "Image Captioning", **disable** "Automatically caption images", as GIC overrides the default caption behavior.
- Chat with a bot a little bit to get some context going.
- Send an image! If GetContext is installed, GIC will pick up on it, and automatically caption images from any message when they're sent, regardless of who sends them. If GIC is not installed, then click the "Grounded Caption" button whenever you send an image. GIC will disable automatic captioning. If you later install GetContext, you'll have to manually re-enable the "execute on user/AI message" boxes in the Quick Reply menu.

Known issues and limitations:

- I am unaware of any way to attach the caption to the image directly in STscript, without also sending a duplicate image. So rather than do it the normal way, GIC simply inserts the caption as a system message at depth 0.
- The "verify caption" dialogue had to be recreated with a popup, but I have no easy way to send the caption back or redo it for the moment ("OK" and "Cancel" both do the same thing; there's no Whiptail-like flow control with them.)
- (The above two points could be ameliorated by simply deleting the message and effectively replacing it with the captioned one, but that feels like it would break pretty easily, and that is not fail-safe behavior...)
- Compiling history can take a little bit.
- Currently, the QR does not take context limits into account. The only ways I could find to do this kept breaking on me. For some reason I insisted on having the entries be a list rather than a flat string, so /trimtokens doesn't work. I'll see if just having them be a flat string is as bad as my brain was certain it was at the time.
- Message Template is currently ignored, and the caption sent plainly.
