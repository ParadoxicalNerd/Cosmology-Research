# The hidden signature of the Baryon Acoustic Oscillations in the Galaxy Temperatures

> The following research project was conducted during the months of June, and July 2019 and was targeted to be published in the Journal Of Emerging Investigators (JEI). The research was conducted without a mentor and lacked sophistication in multiple areas which was not deemed to be publishable in the journal. Yet, I believe that there is virtue in putting this on the internet so that it might help someone in the future. The author, Pankaj Meghani, is uploading this document in good faith on the internet and assumes that it will not be used for any personal gain. Also, if you do use it for personal gain, you are not going to get much further due to its ill written nature and frankly, you can do better than this.

# Introduction
>If you are not familiar with what Baryon Acoustic Oscillations are, do not worry. The following video by PBS Spacetime explains the concepts in a somewhat layperson’s manner which is an interesting watch: https://www.youtube.com/watch?v=PPpUxoeooZk&t=776s. One with a basic understanding of high school level physics and a bit of popular science, should be able to understand the video. Another amazing resource is https://adh-sj.info/bao_cmb.php. The web page has interactive simulations that can help you grasp the concepts intuitively.

>Also, I have “stolen” the abstract from my paper. At places where I felt that it was required, I have added additional details for simpler understanding in the brackets. I have also expanded it for a more intuitive understanding.

Baryonic Acoustic Oscillations have been known to show their effect on the clustering of galaxies (how close they are to every other galaxy in 3d space) and as temperature anisotropies (irregularities) in the cosmic microwave background. This study aims to see whether this clustering can also be found in the mass distribution of the galaxies (do the clumping in space, and the clumping of mass follow a relationship). Five hundred galaxies between redshifts (a measurement of how far stars are from us) 0.45 and 1.0 and between -90 to 90, ra and dec (the area is a circle with its center at 0degrees and a radius of 90degrees) taken from the Sloan Digital Sky Survey DR15 (a catalog of galaxies available to the public) are evaluated using three separate procedures (galaxy clustering, temperature distribution, and temperature difference distribution) in a Jupyter notebook (Python3). Then, galaxy distribution data was estimated from to generate 500 galaxies, which were then analyzed in the same manner. The two were then compared. It is hypothesized that the mass distribution in the galaxies would be affected due to dissimilarities between the concentration of observable matter, dark matter, and radiation pressure in the primordial universe. The results support this hypothesis.

This study aims to investigate whether the amount matter in galaxies is distributed according to their position in the density wave. There should be three peaks on the graph between the mass differences: one for the center, one for the edge of the wave, and one for the intersection of wave fronts. Because of limitations of the catalog, it is not possible to directly measure mass. That said, we can use the temperature of the galaxy as an indicator of its mass. The following analogy should help:

It is a well known fact that the color of a flame depends on its temperature: Cooler flames are yellower while warmer flames are whitish/bluish. Let us say that you have a thousand candles of varying flame colors. You put them around each other, and take a photograph from very far away. The result? The color seen would be the average of the colors of the individual flames. The higher frequency light from the bluer candles will mix from the lower frequency light from the yellower candles, to give a color than corresponds to the average temperature. The same principle applies to stars and thereby galaxies. There is one slight problem to this naive method, that is, it is not possible to tell how many star do the galaxies contain. Fortunately, a slight change in our logic can account for this. We know that the intensity of the light inversely varies with the distance. Because we know the distance (through redshift), we can find the actual brightness of the galaxy. As the brightness directly corresponds to the number of stars, we are now able to find both the average temperature of stars and how many of them are there. Because temperature and the masses of the stars are directly proportional [Salaris, Maurizio; Santi Cassisi (2005). Evolution of stars and stellar populations], we can get the mass of the galaxy.

# Summary of the procedure:
First, we choose the 500 galaxies closest to us. I use SkyServer's SkyQuery Tool for this. The following is the SQL search I used for this:

```sql
SELECT p.objid,
       p.ra,
       p.dec,
       p.u,
       p.g,
       p.r,
       p.i,
       p.z,
       s.z AS redshift INTO mydb.MyTable
FROM galaxy p,
     specobj s
WHERE p.objid=s.bestobjid
  AND s.class = 'GALAXY'
  AND s.sourceType='GALAXY'
  AND p.ra > -90
  AND p.ra < 90
  AND p.dec >-90
  AND p.dec < 90
ORDER BY redshift DESC
```

Then using the above procedure, we are able to estimate the mass of the galaxies. After this, it was trivial work, though quite processing intensive (over 125250 calculations), to be able to compute the mass difference between each one of them [A]. To perform a sanity check and to ensure that the data we have is not an anomaly, we perform the already established distance difference method [B]. We first plot [B] on a frequency distribution and see that it follows the established pattern (Note: the lack of data makes it harder to see. We will prove that this is expected a little later). Then, we plot the frequency distribution for [A], which also follows the hypothesis.

Now, to doubly ensure that this was not some ‘fluke’ of the data, we generate data using parameters of our real data. Then, we make this data pass through the same procedure as [B]. By increasing the number to 5000, we do tend to increase the compute-time. Fortunately, by using simple optimizations while generating this data, we are able to rapidly speed up this process. In these 5000 samples, we do see the expected results. We also perform a chi squared test to ensure that our method is correct, and we get a very high confidence result.

# Conclusion
This was a summary of my entire paper. I do go into more depth inside, so feel free to give it a read if you’re curious. In the files I have attached, you will see **most** of my code.

I say most here, because I did not engage in proper code readability and regular backups to GitHub. This is entirely my fault. I am looking for the code in my project directory, but the sad truth is that with over an 80 odd collection of notebooks and scripts, there is a very low chance I shall find it. Regardless, I did learn the important lesson of remembering to push my code.

I hope you find my paper as informative and fun as I did!

# Acknowledgments
I did not get to put this section in the paper, but I really wanted to thank every resource that helped me through.
* The two links above were absolutely paramount to give me the idea of the project
* Johns Hopkins University for making SciServer available to all
* SciHub for allowing me to run through many papers to get a grasp on the topic without breaking a bank
* And The University of Sydney’s Data-driven Astronomy course on Coursera for the technical skills I needed to succeed.
