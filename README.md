## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/jschaefer619/PHIL191VennDocumentation/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

## Introduction & The Approach

Diagrams have the power to communicate information in a visually salient manner.

This project explores the communication of logical relationships, specifically syllogisms, through Venn Diagrams. Loosely, syllogisms are a form of deductive reasoning to arrive at a conclusion based on two or more propositions that are assumed to be true.

An Example   
P1: All humans are mortal    
P2: All philosophers are humans.    

Conclusion: All philosophers are mortal.

Philosopher Sun-Joo Shin, among others, studied and systemetized the use of Venn Diagrams to visually communicate this form of logical reasoning. Here is a diagram demonstrating how the Venn System displays four types of relationships between two sets:






The goal of this project is to great an interactive system that can generate Venn Diagrams from logical sentences. It was motivated by:

Pedagogy - Digital tools provide new affordances for interactive learning. I hope others will utlize and enjoy this tool!

Personal Development - Programming is an exciting way to engage with this material. I would learn new skills along the way.

Thoughts on the systematicity of Venn - Implementing the Venn System computationally serves as a proof of concept. If a rule-based program can create the diagrams, this speaks to the systematicity of the Venn system. On first encounter, Iconic representations seem 'more slippery' compared to symbolic representations. This would challenge that notion.


## Execution

Initially, my impulse was to find a ready-made graphics package with Venn representations. Searches in open-source repositories seemed fruitful. However, many of these packages were designed to handle large volumes of data to represent. This was impressive in many ways - scaling the venn circles to fit ratios between data points was no small task. But ultimately, these packages were too complex and not flexible enough for my purposes.

I spent some time deliberating which programming language to use. Python was highly readable and a favorite of mine, but javascript would seamlessly travel to web. Though I did not have extensive Javascript experience, accessibility was a priority here. Javascript it was. I settled on utilizing the vector.js library to generate the graphics. Though vector.js did not have a large following, it's documentation was readable and importantly, filled with examples of implementation.

The biggest obstacle was deciding how to shade the inside of vector generated circles. Unfortunately, there was no built in function to detect if two shapes were overlapping. I considered finding a more advanced library that was tailored for spatial analysis, but that would complicate this entire process considerably. Then this occured to me:

```
function coordinateInsideCircle (x, y, shape){
	let distanceBetweenCoordinateAndShape = Math.sqrt((Math.pow((x - shape.cx),2)) +  Math.pow((y - shape.cy),2))
	if (distanceBetweenCoordinateAndShape < shape.r)
		return true;
	else 
		return false;
}

```

Through using a pseudo-grid system based on pixel layout and exploiting the distance formula, I could easily determine if a given point was inside a circle. Essentially, the program could 'scan' over a given area containing circles, then "shade" a space apporpiately by generating small circles in given points.

On a higher level, this program would operate by analyzing a logical sentence, then applying rules to designated circles based on the quantifier.

Abstractly, a given logical sentence contains:

The Subject Set
The Predicate Set
The Quantifier

The format is: [Quantifier] [Subject Set] are [Predicate Set]

This program generates circles for each set, then applies rules to their respective circles based on the quantifier

- For ALL quantifier, shade the Subject Set circle in all areas except for the area where the Predicate Set circle ovelaps
- For NO quantifier, shade the area where the Subject Set and Predicate set overlap
- For SOME quantifier, shade the area where ONLY the Subject Set and Predicate set overlap, no overlap with other circles
- For SOME quantifer w/ not, shade ONLY the area of the subject set

To see the source code with comments, view this project's repository.

## Reflections & Improvements

Though rough around this edges, this project did suceed in creating an interactive venn diagram generator for logical sentences.

A strength of my implementation is that, with some GUI expansions, there are no limits on the number of logical sentences that can be expressed. I have limited the number of sentences to four in the current iteration to simplify the GUI. Granted, there are a limited amount of novel statements that can be formed with only four sets in the current sentence format. Additionally, this implementation may lead to longer run times when given a large number of sentences to compute, due to the psudeo-grid method of shading.

In theory, there are 

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/jschaefer619/PHIL191VennDocumentation/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
