---
layout: page
menus: header
title: TDA-UMAP
permalink: /projects/TDA/
---

<h1 style="font-size:3rem"> Modelling Contagion Networks </h2>
<h3> using Topological Data Analysis and Riemannian Manifolds</h3>

<hr />

 <img src="/assets/img/TDA_UMAP/UMAP.jpg" class="img-fluid">

<h1 style="font-size:1.5rem;font-weight:900;">Inferring networks from data | Analyzing attributed graphs</h1>

<p style="font-size:1.1rem"> Varying degrees of isolation are being put into effect in order to contain the COVID-19 pandemic. These range from simply recommending ‘shelter in place’ to complete lockdown of cities and intense testing, contact tracing and individual quarantining. Epidemiologists and governments are struggling to achieve a balance between these extremes, and an invaluable tool in this effort is simulating the spread under different assumptions. The latest work on this front is presented in work from Google and Tel Aviv University (Reich, Shalev, & Kalvari, 2020), where the authors show, among other conclusions, the influence of people with a large number of connections, and the impact of different policies. These insights can significantly guide policy responses to new and existing outbreaks in a city. The overall setup for the simulation is as shown in the following schematic.</p>

<p>
<img src="/assets/img/TDA_UMAP/before_flowchart.png" class="img-fluid">
</p>
<i>Figure 1: Current Network Simulation Setup</i>

<p style="font-size:1.1rem">A major drawback of this and other network simulations is a lack of an underlying graph that accurately captures the scenario being modelled. Simulations are done on randomly generated structures, and (valuable) conclusions are drawn from these outcomes. We posit that while such analyses are useful for general guidelines, they are not effective for specific scenarios. A further shortcoming is that results and recommendations may vary widely with small changes in the underlying graph.</p>
<br/>
<h1 style="font-size:1.5rem;font-weight:900;">What’s missing?</h1>
<p style="font-size:1.1rem">Networks and the epidemiology of directly transmitted infectious diseases are fundamentally linked. The foundations of early epidemiological models were based on population wide random-mixing, but in practice each individual has a finite set of contacts to whom they can pass infection; the ensemble of all such contacts forms local clusters within a network, which in turn make the interactions (or connections between nodes) location-dependent.</p>

<p style="font-size:1.1rem">Knowledge of the structure of the network allows models to compute the epidemic dynamics at the population scale from the individual-level behaviour of infections. Therefore, characteristics of such networks—and how these deviate from the random-mixing norm—have become important applied concerns that may enhance the understanding and prediction of epidemic patterns and intervention measures.</p>

<br/>
<h1 style="font-size:1.5rem;font-weight:900;">Uniform Manifold Approximation and Projection (UMAP)</h1>
<p style="font-size:1.1rem">Orthogonal to these agent-based simulations for epidemiology is the field of topological data analysis (Chazal & Michel, 2017), which infers hidden information about the structure of a complex and noisy data set using ideas from topology and geometry. TDA has been applied to the study of progression analysis of disease, signal analysis, propagation of contagions in a network, imaging and remote sensing.</p>

<p style="font-size:1.1rem">One of the recent approaches for dimensionality reduction that is inspired from TDA is the Uniform Manifold Approximation and Projection (UMAP). UMAP learns the underlying topology of a point-cloud data, and tries to project it down to a lower-dimensional manifold with a near-similar topology. The results of UMAP, shown in Figure 2, demonstrate the efficacy of TDA. Taking the handwritten MNIST data set as our input, clustering using k-means forms clusters shown on the left. However, UMAP is able to perform non-linear manifold aware dimension reduction to obtain the clusters shown on the right. We anticipate similar success using location, gender and health data of individuals to use in the network simulations.</p>

<p>
<img src="/assets/img/TDA_UMAP/mnist.png" class="img-fluid">
</p>
<i>Figure 2: Clustering on MNIST using K-Means (left) and TDA/UMAP (right)</i>

<br/>
<p style="font-size:1.1rem">In this work, we propose to use only the first part of UMAP that employs TDA – let us call it UMAP-R. We apply UMAP-R to location data of individuals to develop networks that represent ‘ground truth’, which can then be used for agent-based simulations to analyse and predict the spread of COVID-19. Figure 3 shows how UMAP-R is integrated into the existing setup.</p>

<p>
<img src="/assets/img/TDA_UMAP/after_flowchart.png" class="img-fluid">
</p>
<i>Figure 3 Using Topological Data Analysis to model the graph</i>

<br/>
<h1 style="font-size:1.5rem;font-weight:900;">How does UMAP form connections between nodes in a graph?</h1>
<i style="font-size:1rem;font-weight:900;"> [The following explanation and supporting figures are presented from the excellent"<a href="https://umap-learn.readthedocs.io/en/latest/#">UMAP Documentation</a> "by" <a href="https://arxiv.org/search/stat?searchtype=author&amp;query=McInnes%2C+L">Leland McInnes</a>"]" </i>
<br/>
<h1 style="font-size:1.1rem">Topological Data Analysis and Simplicial Complexes</h1>
<p style="font-size:1.1rem">Simplicial complexes are a means to construct topological spaces out of simple combinatorial components. This allows one to reduce the complexities of dealing with the continuous geometry of topological spaces to the task of relatively simple combinatorics and counting. This method of taming geometry and topology will be fundamental to our approach to topological data analysis in general, and dimension reduction in particular.</p>

<p style="font-size:1.1rem">"The first step is to provide some simple combinatorial building blocks called" <em>simplices</em>:</p>

<p>
<img src="/assets/img/TDA_UMAP/simplices.png" class="img-fluid">
</p>
<p>
<img src="/assets/img/TDA_UMAP/sine1.png" class="img-fluid">
</p>
<i>Test data set of a noisy sine wave</i>
<p>
<img src="/assets/img/TDA_UMAP/sine2.png" class="img-fluid">
</p>
<i>A basic open cover of the test data</i>
<p>
<img src="/assets/img/TDA_UMAP/sine3.png" class="img-fluid">
</p>
<i>A simplicial complex built from the test data</i>
<br/>

<p style="font-size:1.1rem">There are two things to note here: first, the simplicial complex does a reasonable job of starting to capture the fundamental topology of the dataset; second, most of the work is really done by the 0- and 1-simplices, which are easier to deal with computationally.</p>

<br/>
<h1 style="font-size:1.1rem">Why use Topology?</h1>
<p style="font-size:1.1rem">The first reason is that the topological approach, while abstract, provides sound theoretical justification for what we are doing. While building a neighborhood-graph and laying it out in lower dimensional space makes heuristic sense and is computationally tractable, it doesn’t provide the same underlying motivation of capturing the underlying topological structure of the data faithfully.</p>

<p style="font-size:1.1rem">The second reason is that it is this more abstract topological approach that will allow us to generalize the approach.</p>

<br/>
<h1 style="font-size:1.1rem">Adapting to Real World Data</h1>
<p style="font-size:1.1rem">If we consider data that is uniformly distributed, the resulting open cover looks pretty good:</p>

<p>
<img src="/assets/img/TDA_UMAP/sine4.png" class="img-fluid">
</p>
<i>Open balls over uniformly distributed data</i>
<br/>

<p style="font-size:1.1rem">Because the data is evenly spread we actually cover the underlying manifold and don’t end up with clumping. In other words, all this theory works well assuming that the data is uniformly distributed over the manifold. However, real-world data/spatial data under consideration isn’t that nicely behaved.</p>

<p style="font-size:1.1rem">How can we resolve this? By turning the problem on its head: assume that the data is uniformly distributed on the manifold, and ask what that tells us about the manifold itself. If the data looks like it isn’t uniformly distributed that must simply be because the notion of distance is varying across the manifold.</p>
<p style="font-size:1.1rem">By assuming that the data is uniformly distributed we can actually compute (an approximation of) a local notion of distance for each point by making use of a little standard Riemannian geometry.
Hence, the open balls are structured such that the radius is larger in sparse regions and smaller in concentrated regions. The radius is fixed to unit distance in the riemannian terms, thus, keeping our manifold uniformly distributed.
Each point is given its own unique distance function, and we can simply select balls of radius one with respect to that local distance function!</p>

<p>
<img src="/assets/img/TDA_UMAP/sine5.png" class="img-fluid">
</p>
<i>Open balls of radius one with a locally varying metric</i>
<br/>

<p style="font-size:1.1rem">Of course, we have traded choosing the radius of the balls for choosing a value for k. However it is often easier to pick a resolution scale in terms of number of neighbors than it is to correctly choose a distance. This is because choosing a distance is very dataset dependent: one needs to look at the distribution of distances in the dataset to even begin to select a good value. In contrast, while a k value is still dataset dependent to some degree, there are reasonable default choices, such as the 10 nearest neighbors, that should work acceptably for most datasets.</p>

<p style="font-size:1.1rem">At the same time the topological interpretation of all of this gives us a more meaningful interpretation of k. The choice of k determines how locally we wish to estimate the Riemannian metric. A small choice of k means we want a very local interpretation which will more accurately capture fine detail structure and variation of the Riemannian metric. Choosing a large k means our estimates will be based on larger regions, and thus, while missing some of the fine detail structure, they will be more broadly accurate across the manifold as a whole, having more data to make the estimate with.</p>

<p style="font-size:1.1rem">We also get a further benefit from this Riemannian metric based approach: we actually have a local metric space associated to each point, and can meaningfully measure distance, and thus we could weight the edges of the graph we might generate by how far apart (in terms of the local metric) the points on the edges are. In slightly more mathematical terms we can think of this as working in a fuzzy topology where being in an open set in a cover is no longer a binary yes or no, but instead a fuzzy value between zero and one. Obviously the certainty that points are in a ball of a given radius will decay as we move away from the center of the ball. We could visualize such a fuzzy cover as looking something like this:</p>

<p>
<img src="/assets/img/TDA_UMAP/sine6.png" class="img-fluid">
</p>
<i>Fuzzy open balls of radius one with a locally varying metric</i>
<br/>

<p style="font-size:1.1rem">One of the assumptions that we need to make for riemannian geometry is that our data must be locally connected. Simply put, no point must be completely isolated from the rest of the data. To ensure this, we can implement this by simply having the fuzzy confidence decay in terms of distance beyond the first nearest neighbor. We can visualize the result as:</p>

<p>
<img src="/assets/img/TDA_UMAP/sine7.png" class="img-fluid">
</p>
<i>Decaying Fuzzy Confidence</i>
<br/>

<p style="font-size:1.1rem">OFrom a practical standpoint – in high dimensions distances tend to be larger, but also more similar to one another (the curse of dimensionality). This means that the distance to the first nearest neighbor can be quite large, but the distance to the tenth nearest neighbor can often be only slightly larger (in relative terms). The local connectivity constraint ensures that we focus on the difference in distances among nearest neighbors rather than the absolute distance (which shows little differentiation among neighbors).</p>

<p style="font-size:1.1rem">Lastly, between any two points we might have up to two edges and the weights on those edges disagree with one another. Mathematically we actually have a family of fuzzy simplicial sets, and the obvious choice is to take their union – a well-defined operation.</p>

<p style="font-size:1.1rem">In graph terms what we get is the following: if we want to merge together two disagreeing edges with weight a and b then we should have a single edge with combined weight a+b−a⋅b.</p>

<p style="font-size:1.1rem">The way to think of this is that the weights are effectively the probabilities that an edge (1-simplex) exists. The combined weight is then the probability that at least one of the edges exists.</p>

<p style="font-size:1.1rem">If we apply this process to union together all the fuzzy simplicial sets we end up with a single fuzzy simplicial complex, which we can again think of as a weighted graph.</p>

<p>
<img src="/assets/img/TDA_UMAP/sine8.png" class="img-fluid">
</p>
<i>Graph with combined edge weights</i>
<br/>

<h1 style="font-size:1.1rem">Epidemic Modeling using SEIR Compartment Model</h1>
<p style="font-size:1.1rem">The above obtained structure-aware graph network is fed to an SEIR Model to obtain corresponding epidemic curves.</p>

<p>
<img src="/assets/img/TDA_UMAP/seir.png" class="img-fluid">
</p>
<i>SEIR model of infectious disease</i>
<br/>


<p style="font-size:1.1rem">The rates of transition between the states are given by the parameters:
σ: rate of progression (inverse of incubation period)
γ: rate of recovery (inverse of infectious period)
ξ: rate of re-susceptibility (inverse of temporary immunity period; 0 if permanent immunity)
μI: rate of mortality from the disease (deaths per infectious individual per time)</p>

<p style="font-size:1.1rem">Sample Output:</p>
<p>
<img src="/assets/img/TDA_UMAP/seir0.png" class="img-fluid">
</p>
<i>SEIR plot</i>
<br/>

<p style="font-size:1.1rem">[Coming Soon: Comparative analysis of epidemic curves of our TDA/UMAP based model vs models involving random connections]</p>






<p> Lets try the different text styles  <b> Bold </b> , <strong> Strong </strong>, <em> Emphasis </em>, <i> Italic </i> </p>


<p> Now, lets try different heading styles : </p>

<h1> Hello in h1 ! </h1>
<h2> Hello in h2 ! </h2>
<h3> Hello in h3 ! </h3>
<h4> Hello in h4 ! </h4>
<h5> Hello in h5 ! </h5>
<h6> Hello in h6 ! </h6>

<hr />
<p> Unordered List </p>

<ul>
<li> List Item 1 </li>
<li> List Item 2 </li>
<li> List Item 3 </li>
<li> List Item 4 </li>
<li> List Item 5 </li>
</ul>

<p> Ordered List </p>
<ol>
<li> List Item 1 </li>
<li> List Item 2 </li>
<li> List Item 3 </li>
<li> List Item 4 </li>
<li> List Item 5 </li>
</ol>

<blockquote>
<p>This is a Block Quote,  It can Expand Multiple Lines </p>

</blockquote>

<p>You can use the mark tag to <mark>highlight</mark> text. </p>

<p><del> This line of text is meant to be deleted text </del> </p>

<p><u>This line of text will render as underlined</u></p>
<p><small>This line of text is meant to be treated as fine print.</small></p>
<p><strong>This line rendered as bold text.</strong></p>
<p><em>This line rendered as italicized text.</em></p>
<p><abbr title="attribute">attr</abbr></p>
<p><abbr title="HyperText Markup Language" class="initialism">HTML</abbr></p>

<hr />
<div class="responsive-table">
<table>
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Heading</th>
          <th scope="col">Heading</th>
          <th scope="col">Heading</th>
          <th scope="col">Heading</th>
          <th scope="col">Heading</th>
          <th scope="col">Heading</th>
          <th scope="col">Heading</th>
          <th scope="col">Heading</th>
          <th scope="col">Heading</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th scope="row">1</th>
          <td>Cell</td>
          <td>Cell</td>
          <td>Cell</td>
          <td>Cell</td>
          <td>Cell</td>
          <td>Cell</td>
          <td>Cell</td>
          <td>Cell</td>
          <td>Cell</td>
        </tr>
        <tr>
          <th scope="row">2</th>
          <td>Cell</td>
          <td>Cell</td>
          <td>Cell</td>
          <td>Cell</td>
          <td>Cell</td>
          <td>Cell</td>
          <td>Cell</td>
          <td>Cell</td>
          <td>Cell</td>
        </tr>
        <tr>
          <th scope="row">3</th>
          <td>Cell</td>
          <td>Cell</td>
          <td>Cell</td>
          <td>Cell</td>
          <td>Cell</td>
          <td>Cell</td>
          <td>Cell</td>
          <td>Cell</td>
          <td>Cell</td>
        </tr>
      </tbody>
    </table>
    </div>

<hr />

<h3>YouTube Responsive Embed</h3>

<iframe width="560" height="315" src="https://www.youtube.com/embed/nuwjUZCSB2Y?rel=0&amp;controls=0&amp;showinfo=0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen=""></iframe>

<hr />

<h3>Vimeo Responsive Embed</h3>

<iframe src="https://player.vimeo.com/video/212114694?title=0&amp;byline=0&amp;portrait=0" width="640" height="360" frameborder="0" webkitallowfullscreen="" mozallowfullscreen="" allowfullscreen=""></iframe>

<hr />

<h3 id="ted-responsive-embed">TED Responsive Embed</h3>

<iframe src="https://embed.ted.com/talks/ted_halstead_a_climate_solution_where_all_sides_can_win" width="640" height="360" frameborder="0" scrolling="no" allowfullscreen=""></iframe>

<hr />

<h3 id="twitch-responsive-embed">Twitch Responsive Embed</h3>

<iframe src="https://player.twitch.tv/?autoplay=false&amp;video=v248755437" frameborder="0" allowfullscreen="true" scrolling="no" height="378" width="620"></iframe>

<hr />

<h3 id="soundcloud-embed">SoundCloud Embed</h3>

<iframe width="100%" height="166" scrolling="no" frameborder="no" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/29738591&amp;color=ff5500&amp;auto_play=false&amp;hide_related=false&amp;show_comments=true&amp;show_user=true&amp;show_reposts=false"></iframe>

<hr />

<h3 id="codepen-embed">CodePen Embed</h3>

<p data-height="265" data-theme-id="light" data-slug-hash="YWvpRo" data-default-tab="css,result" data-user="kharrop" data-embed-version="2" data-pen-title="Referral Form" class="codepen"></p>
<script async="" src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

<hr />

<h3 id="syntax-highlighting">Syntax Highlighting</h3>

<figure class="highlight"><pre><code class="language-js" data-lang="js"><span class="s1">'use strict'</span><span class="p">;</span>
<span class="kd">var</span> <span class="nx">markdown</span> <span class="o">=</span> <span class="nx">require</span><span class="p">(</span><span class="s1">'markdown'</span><span class="p">).</span><span class="nx">markdown</span><span class="p">;</span>
<span class="kd">function</span> <span class="nx">Editor</span><span class="p">(</span><span class="nx">input</span><span class="p">,</span> <span class="nx">preview</span><span class="p">)</span> <span class="p">{</span>
  <span class="k">this</span><span class="p">.</span><span class="nx">update</span> <span class="o">=</span> <span class="kd">function</span><span class="p">()</span> <span class="p">{</span>
    <span class="nx">preview</span><span class="p">.</span><span class="nx">innerHTML</span> <span class="o">=</span> <span class="nx">markdown</span><span class="p">.</span><span class="nx">toHTML</span><span class="p">(</span><span class="nx">input</span><span class="p">.</span><span class="nx">value</span><span class="p">);</span>
  <span class="p">};</span>
  <span class="nx">input</span><span class="p">.</span><span class="nx">editor</span> <span class="o">=</span> <span class="k">this</span><span class="p">;</span>
  <span class="k">this</span><span class="p">.</span><span class="nx">update</span><span class="p">();</span>
<span class="p">}</span></code></pre></figure>

<p>You can add inline code just like this, E.g. <code class="highlighter-rouge">.code { color: #fff; }</code></p>

<figure class="highlight"><pre><code class="language-css" data-lang="css"><span class="nt">pre</span> <span class="p">{</span>
  <span class="nl">background-color</span><span class="p">:</span> <span class="m">#f4f4f4</span><span class="p">;</span>
  <span class="nl">max-width</span><span class="p">:</span> <span class="m">100%</span><span class="p">;</span>
  <span class="nl">overflow</span><span class="p">:</span> <span class="nb">auto</span><span class="p">;</span>
<span class="p">}</span></code></pre></figure>

<hr />

<h3 id="github-gist-embed">GitHub gist Embed</h3>

<script src="https://gist.github.com/ahmadajmi/dbb4f713317721668bcbc39420562afc.js"></script>

<hr />

<h3 id="input-style">Input Style</h3>

<p><input type="text" placeholder="I'm an input field!" /></p>

<hr />

<h3> Twitter Embed </h3>

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">I just published “Deploying a blog using Jekyll and Github Pages with SSL certificate for Free” <a href="https://t.co/B3T3IQVU93">https://t.co/B3T3IQVU93</a></p>&mdash; Sujay Kundu (@SujayKundu777) <a href="https://twitter.com/SujayKundu777/status/1012601950469160962?ref_src=twsrc%5Etfw">June 29, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

<hr />

<h3> Instagram Embed </h3>

<blockquote class="instagram-media" data-instgrm-permalink="https://www.instagram.com/p/BhFTg6uhNRi/" data-instgrm-version="9" style=" background:#FFF; border:0; border-radius:3px; box-shadow:0 0 1px 0 rgba(0,0,0,0.5),0 1px 10px 0 rgba(0,0,0,0.15); margin: 1px; max-width:658px; min-width:326px; padding:0; width:99.375%; width:-webkit-calc(100% - 2px); width:calc(100% - 2px);"><div style="padding:8px;"> <div style=" background:#F8F8F8; line-height:0; margin-top:40px; padding:50.0% 0; text-align:center; width:100%;"> <div style=" background:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACwAAAAsCAMAAAApWqozAAAABGdBTUEAALGPC/xhBQAAAAFzUkdCAK7OHOkAAAAMUExURczMzPf399fX1+bm5mzY9AMAAADiSURBVDjLvZXbEsMgCES5/P8/t9FuRVCRmU73JWlzosgSIIZURCjo/ad+EQJJB4Hv8BFt+IDpQoCx1wjOSBFhh2XssxEIYn3ulI/6MNReE07UIWJEv8UEOWDS88LY97kqyTliJKKtuYBbruAyVh5wOHiXmpi5we58Ek028czwyuQdLKPG1Bkb4NnM+VeAnfHqn1k4+GPT6uGQcvu2h2OVuIf/gWUFyy8OWEpdyZSa3aVCqpVoVvzZZ2VTnn2wU8qzVjDDetO90GSy9mVLqtgYSy231MxrY6I2gGqjrTY0L8fxCxfCBbhWrsYYAAAAAElFTkSuQmCC); display:block; height:44px; margin:0 auto -44px; position:relative; top:-22px; width:44px;"></div></div><p style=" color:#c9c8cd; font-family:Arial,sans-serif; font-size:14px; line-height:17px; margin-bottom:0; margin-top:8px; overflow:hidden; padding:8px 0 7px; text-align:center; text-overflow:ellipsis; white-space:nowrap;"><a href="https://www.instagram.com/p/BhFTg6uhNRi/" style=" color:#c9c8cd; font-family:Arial,sans-serif; font-size:14px; font-style:normal; font-weight:normal; line-height:17px; text-decoration:none;" target="_blank">A post shared by Ahmad Ajmi (@ahmadajme)</a> on <time style=" font-family:Arial,sans-serif; font-size:14px; line-height:17px;" datetime="2018-04-02T21:18:58+00:00">Apr 2, 2018 at 2:18pm PDT</time></p></div></blockquote> <script async defer src="//www.instagram.com/embed.js"></script>

