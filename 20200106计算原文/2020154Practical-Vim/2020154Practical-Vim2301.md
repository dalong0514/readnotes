Keep working at it. With practice, things that once seemed tricky will become second nature. Make it your goal to operate Vim without having to think about what you’re doing. When you reach that level, you’ll be able to edit text at the speed of thought.

Practical Vim doesn’t intend to provide a linear reading experience, so you won’t have taken everything in on your first pass. Some of the tips are basic, while others speak to the advanced user. I expect that you’ll be able to pick up this book again and learn something new.

Make Vim Your Own

	 	 We’ve been working with stock Vim pretty much as it runs out of the box. The factory settings have served as a useful baseline, giving us a common feature set to work with, but I don’t mean to suggest that you stick with them. Vim has some unfortunate default settings. If you want to know why something behaves a certain way, the answer often seems to be,「Because that’s how vi did it!」

	 	 But you don’t need to put up with those defaults. You can customize Vim to make it behave the way you want. If you save your preferences in a vimrc file, you can make it so that Vim is always configured in a way that suits your workflow. Appendix 1, ​Customize Vim to Suit Your Preferences​, provides a basic primer to get you started.

Know the Saw, Then Sharpen It

	 	 In Bram Moolenaar’s classic essay「Seven Habits of Effective Text Editing,」he advises that you invest time sharpening the saw.[31] Building your vimrc file is one way to do that, but it’s vital that you understand Vim’s baseline functionality before you build on top of it. First learn to use the saw. Then sharpen it.

I’ve seen people customizing Vim in ways that blunt the saw. I’ve even seen people sharpening the wrong edge! Don’t worry; because you’ve read Practical Vim, you’re not going to make those same mistakes. You already know Vim’s core functionality.

	 Build your vimrc from scratch. As a starting point, you could use the essential.vim file that’s distributed with this book’s source code. Many Vim users publish their vimrc files on the Internet, and they can be a great source for inspiration. Copy the parts that solve your problems, but leave behind what you don’t need. You should own your vimrc. That means understanding what’s in it.

	 	 I’ve resisted the temptation to share the best bits from my vimrc (had I done so, this book would be double the length), but I’ve dropped hints in the occasional sidebar. You can find my vimrc file on github, along with many of my dotfiles.[32] I’ve also documented some of my customizations at Vimcasts.org, where I also recommend some of my favorite plugins.[33]

Vim has an unusual license: it’s distributed as charityware (licenseⓘ). That means that you can use it freely, but you are encouraged to make a donation to the ICCF Holland foundation,[34] which helps needy children in Uganda. Please show your thanks to Vim’s authors by pledging something toward this worthy cause.

​=> ​:x​

Footnotes

[31]

http://www.moolenaar.net/habits.html

[32]

http://github.com/nelstrom/dotfiles

[33]

http://vimcasts.org/

[34]

http://iccf-holland.org/

Copyright © 2016, The Pragmatic Bookshelf.

Appendix 1

Customize Vim to Suit Your Preferences

