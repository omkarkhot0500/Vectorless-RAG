## Traditional Vector RAG vs. PageIndex (Vectorless RAG)
![alt text](Gemini_Generated_Image_6rkr3i6rkr3i6rkr.png)


What is this diagram showing?
This image compares two different ways an AI can search through a massive document to answer a user's question. On the left is the older, standard method (Traditional Vector RAG), and on the right is a newer, smarter approach (PageIndex / Vectorless RAG).

How the Flow Works (Step-by-Step)
The Input: Both systems start with the same thing—a long PDF document (like a 100-page financial report) and a user asking a question.

The Indexing & Storage (The "Brain" Setup):

Traditional RAG (Left): It takes the PDF, chops it into random, equal-sized pieces (Chunking), and turns those pieces into math formulas (Embeddings). It saves these in a Vector Database. Think of this like cutting a book into random paragraphs and scattering them in a box.

PageIndex (Right): Instead of chopping it up randomly, an LLM acts like a human reader. It scans the document and builds an organized table of contents (LLM tree builder) saved as a JSON tree index. No complex math database is needed.

Retrieval (Finding the Answer):

Traditional RAG: When you ask a question, it converts your question into math and looks for chunks with similar math formulas (ANN search). It pulls out Flat text chunks but has no idea where they came from or what the surrounding pages say.

PageIndex: When you ask a question, the LLM looks at the table of contents tree it built (LLM tree search). It logically reasons: "Ah, this question is about international laws, so I should look under Section 4, Page 28." It pulls out Named sections with full context.

The Output:

Traditional RAG gives you a raw answer but cannot tell you exactly what page it found it on because the structural context was lost. It relies on similarity search (what looks closest, not necessarily what is right).

PageIndex gives you a precise answer complete with page and section citations. It relies on reasoning-based retrieval (navigating like a human expert).


## Inside the PageIndex Tree Builder Workflow

![alt text](Gemini_Generated_Image_cve8zscve8zscve8.png)

What is this diagram showing?This image zooms into the right side of the first diagram. It explains exactly how the AI acts like a human librarian to build that smart, organized map (the JSON tree index) out of a raw PDF.How the Flow Works (Step-by-Step)Raw PDF Document: You give the system a long, structured document.TOC (Table of Contents) Detection: The AI first scans the top of the document to see if a Table of Contents already exists.Branch A (Has TOC): If it finds one, it copies it directly to understand how the chapters are broken down.Branch B (No TOC): If there isn't one, an LLM reads through the pages and guesses what the headings and structure should be based on the text size and layout.Section-Aware Splitting: Instead of cutting text mid-sentence or mid-paragraph based on a character limit (which traditional RAG does), this system splits the document only where a section naturally ends. It respects logical boundaries.LLM Summarizes Each Section: The AI reads every individual section and creates a mini ID card for it, including a unique node_id, the title, the exact page number, and a short summary of what that section is about.Assemble Hierarchical Tree: Finally, it links everything together into a family tree structure (Parent $\rightarrow$ Child $\rightarrow$ Grandchild).Example: As shown in the dotted box, "Financial Stability" (Page 21) is the parent chapter. Nested directly underneath it are its sub-sections: "Monitoring vulnerabilities" (Pages 22–28) and "International cooperation" (Pages 28–31).



![alt text]({C3390988-5BBF-4DEB-B49C-07B20956DC0E}.png)