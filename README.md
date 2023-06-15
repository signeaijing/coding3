# README 
Link to repository: https://github.com/signeaijing/coding3
Link to video demonstration: https://youtu.be/C9Fa9R_fD6s

## CONTEXT OF PROJECT
This project is inspired by the nüshu characters of the Jiangyoung dialect, Yang Zhuang (often called tuhua, 
but that term refers to an inferior language) in the province of Hunan, China. The word, translating literally to 
‘women’s script’, was developed by and for women in the Shang or Song dynasty, a time when women were 
not allowed inside schools and institutions. (Lofthouse, 2020)

It was used by Han, Maio and Yao people and passed down through generations. Therefore, the variations of 
the scripts are many as each area and each woman would develop their own version that would pass down 
through generations. (Lofthouse, 2020) Yang Huanyi, the last fluent speaker of the language died in 2004 and 
therefore the documentation around the script is very limited. 

I am drawn to the fluidity and autonomy that lies in this. The aim of this project is to showcase this. I will do 
this by training DCGAN using this guide: https://pytorch.org/tutorials/beginner/dcgan_faces_tutorial.html
(other resources are referenced in the notebook) and then creating an animation based on the generated images, 
emphasizes how oral practices and dead languages creates gaps between the people who created it and those 
today. 

## GETTING THE DATA
This was the first issue: That there was no dataset available, and the images that I found available to scrape 
was of very poor quality. I did manage to find unicodes for the script, but I never managed to display it in a 
notebook even though I tried downloading the .tff files, installing them, converting unicodes and loading in 
one at a time. The .csv file didn’t even show it either. 

I ended up finding an image containing the characters with unicodes in a grid. I asked ChatGPT to generate 
code that could split the image into rows x columns of the grid, which provided me with 397 images each 
depicting one character. 

Due to this not being enough data to train on, I used the dataset-tools repository that works through the 
command line to datawrangle. Repo: https://github.com/dvschultz/dataset-tools

See following pictures: 
This produced a dataset of 1588 images. 
Figure 1 data after wrangling
Then I trained on the DCGAN - see .ipynb notebook for details. 
RESULTS
First I got super bad results. The loss output started at around 30 and ended at for the generator and 18 for the 
discriminator. The output of images was also not good, and the loss for generator and discriminator was 
horrible. 
Also the confidence for the discriminator was a 100 percent from the get go for both fake and real images. 
Therefore, I played around with the 
hyperparameters like the learning rate, the 
beta1 parameter for the optimizer, the size of 
the feature maps for both the generator and 
the discriminator going between 8 and 64 in 
order to capture more details. I also trained 
for between 20-60 epochs. I thought of 
implementing an early stop, but from this 
website, I learned that it might have very 
insignificant impact on the training. 
https://towardsdatascience.com/10-lessonsi-learned-training-generative-adversarialnetworks-gans-for-a-year-c9071159628
I got the same results each time, with only 
minor improvements in the aesthetics. 
However, the loss and confidence did 
improve a lot. 
This is the results from the final training. 
Outcome for the loss for both generator and 
discriminator goes down while still being quite 
stable, as well as the confidence for the 
discriminrator goes up. However, the generated 
pictures are still not really looking like the 
training managed to capture the main features of 
the project. 
FINAL REFLECTIONS 
The outcome of this project is mildly very disappointing. However, I do know that my intentions and methods 
could have been sharper. There was a clear obstacle in the language barrier - my mandarin is horrendous as 
well as the Jiangyoung dialect being very hard to understand, forcing me to derive to aesthetic from my initial 
intention of making a translation/language-based project. 
The images are quite simple and are all black and white resulting in very limited diversity in the generated 
tensors. Also, I have a feeling that that might make the training a bit weird, as the discriminator quite quickly 
becomes very good. 
If I were to try to carry out this project again, I would probably train on a completely different model. 
Additional note added on 16th June: 
I JUST stumbled upon this project interpolating between traditional Chinese characters and then trying to 
incorporate Hangul - the characters used for Korean script. This would have been the perfect model to use for 
this project, but unfortunately, I discovered it too late to do it for this deadline. Project can be found here: 
https://kaonashi-tyc.github.io/2017/04/06/zi2zi.html
REFERENCES 
Lofthouse, A. (2020). Nüshu: China’s secret female-only language. BBC Travel. Retrieved 8th June from 
https://www.bbc.com/travel/article/20200930-nshu-chinas-secret-female-only-language
