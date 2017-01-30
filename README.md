ATTENTION VISUALIZER BY ABIGAIL SEE
abisee@stanford.edu

To run the visualizer, run
  python -m SimpleHTTPServer
from this directory then navigate to
  http://localhost:8000/
in browser.


To visualize your own weights, you need to create a file called attn_wts.json that has the following fields:

  article_lst: the article as a list of words
  decoded_lst: the decoded summary as a list of words
  abstract_str: the reference summary as a single string
  attn_wts: a list same length as decoded_lst, containing lists of length "attention length", containing probabilities.
    Note attention length must be <= length of article_lst.
    e.g. your article may have 500 words but you only fed the first 200 words into the model, thus attention length is 200.
    In this case the visualizer will mark the truncation point in the article.
  gen_probs: a list same length as decoded_lst, containing probabilities.

See the included example attn_wts.json.

WARNING: Make sure that none of the strings in article_lst, decoded_lst, or abstract_str contain <angled brackets>. These will interfere with the HTML and can result in text not being displayed.
