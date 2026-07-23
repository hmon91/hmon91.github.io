---
# ============================================================================
#  HOMEPAGE TOGGLE
#  The homepage ("/") is currently served by the standalone file  /index.html
#  and THIS original AcademicPages page is turned OFF (published: false).
#
#  To switch back to this original homepage:
#    1. Change  published: false  ->  published: true   (or delete that line)
#    2. Uncomment  permalink: /   and the  redirect_from:  block below
#    3. Remove the Liquid comment wrapper around the body (the tag that opens
#       the block just below the front matter, and its matching closing tag
#       at the very end of this file)
#    4. Delete or rename  /index.html  so it no longer claims "/"
# ============================================================================
published: false
# permalink: /
title: "About Me"
excerpt: "About me"
author_profile: true
mathjax: true
# redirect_from:
#   - /about/
#   - /about.html
---
{% comment %}
======================================================================
ORIGINAL HOMEPAGE BODY — DISABLED.
To restore it, delete the tag that opens this block (on the line above)
and its matching closing tag at the very bottom of the file, then follow
the numbered steps in the front matter above.
======================================================================

{% include base_path %}
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>
<script>
  window.MathJax = {
    tex: {
      inlineMath: [['$', '$'], ['\\(', '\\)']]
    }
  };
</script>
I am a **Ph.D. researcher** at Northeastern University developing foundational methods for trustworthy and scalable artificial intelligence in dynamical systems. My work lies at the intersection of **data-driven learning, optimization, and control theory**, with a focus on formal verification, robustness, and safety guarantees for neural-network-based decision-making systems.
I develop theory, algorithms, and software for certifying learning-enabled systems operating in complex, safety-critical environments, with applications spanning autonomous systems and robotics.
<center>
  <img src="/images/frankasiami1.gif" alt="Franka Emika Robot Demo" style="width: 100%; max-width: 500px; border: 1px solid #ddd; padding: 5px; border-radius: 5px;">
</center>
<br>
### Research Highlights
* **Scalable Verification:** Developed a scalable stability and robustness verification pipeline for learning-enabled autonomous systems, achieving up to ~\\(10^4 \times\\) speedup over state-of-the-art methods.
* **Neural Network Bounding:** Introduced novel global and local sector-bounds for Feedforward Neural Networks (FFNNs), enabling depth-agnostic and input-aware bounds with tighter certification than methods like CROWN.
* **Tool Integration:** Integrated verification tools (AutoLIRPA, JAX-Verify) with classical control analysis (Lyapunov methods, MPC) to build reproducible verification workflows.
I am currently working on my thesis: *"Scalable Method for Stability and Robustness Verification of Systems with NN Feedback using Positivity Constraints"*.
{% endcomment %}
