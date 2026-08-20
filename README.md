# Prompt Injection Prevention

## Understanding Prompt Injection

LLMs we're using today are trained on the Transformer architecture. To simplify that, think of them as highly precise sentence auto-completers. Initially, they were designed to predict the next word in the sentence and with feedback, they got better at making more accurate predictions. Today, you talk to them in natural language and they respond back to you in the same.

Since your prompt that LLMs get and the answer they produce are in natural language, manipulating this pipeline also includes using malicious prompts in natural language, and that's what makes it harder to detect.

## Most Common Ways Your Prompts can be Injected

- Direct attacks where someone types a command to trick or override the AI's original rules, usually because user text wasn't safely separated.
- Hidden attacks tucked away inside external files, websites, or documents that the AI reads, tricking it without the user noticing.
- Tricky phrases or mixed messages that confuse the AI so it misinterprets its main instructions and follows bad commands instead.
- Sneaky questions meant to steal secret information, like system settings, internal instructions, or private chats.

## 7 Ways to Protect Against Prompt Injection

### Testing on Python Notebook:

Baseline security practices to prevent workflow corruption:

<img width="1489" height="333" alt="image" src="https://github.com/user-attachments/assets/0febc35a-c01d-4324-ac93-158e1ace8a18" />




1. It uses regular expression filters to intercept and block known command-override signatures instantly.
2. It encapsulates untrusted inputs within strict token tags (USER_DATA_START / USER_DATA_END) to help the model structurally differentiate developer commands from user-supplied data.
3. It embeds high-priority security instructions directly into the prompt stream, explicitly commanding the model never to adopt new personas or obey instructions found inside data blocks.
4. Audits the generated text response after inference to detect whether the model accidentally complied with an injection attempt (e.g., checking for leaked system instructions).

### Bonus

5. Note that, attackers can easily bypass heuristic and pattern matching by using typos, synonyms, non-English languages, zero-width spaces, or encoding tricks (e.g., base64 encoding). Instead of matching exact text patterns, use a smaller, dedicated classification model (like Llama Guard or NeMo Guardrails) to evaluate the intent and semantic meaning of the input.
6. Save your secrets (such as API keys) on server-side and never ship them in the frontend code, so even if your bot is successfully manipulated to give out secrets, it's unable to access your secrets.
7.  Limit the tool access LLMs have while building agents, and keep Human-in-the-Loop approval before crucial writes in your dbs, repos or other data corpora.
