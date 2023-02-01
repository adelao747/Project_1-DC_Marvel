# Project_1
%matplotlib notebook
In [162]:
import pandas as pd
import matplotlib.pyplot as plt
import scipy.stats as st
import numpy as np
In [163]:
dc_data_df= pd.read_csv('../Project_1/dc-wikia-data_csv.csv')
In [164]:
marvel_data_df = pd.read_csv('../Project_1/marvel-wikia-data_csv.csv')
In [165]:
combined_hero_data = pd.merge(dc_data_df, marvel_data_df, how="outer")
In [166]:
combined_hero_data
Out[166]:
	page_id	name	urlslug	id	align	eye	hair	sex	gsm	alive	appearances	first appearance	year
0	1422	batman (bruce wayne)	\/wiki\/batman_(bruce_wayne)	secret identity	good characters	blue eyes	black hair	male characters	straight	living characters	3093.0	1939, may	1939.0
1	23387	superman (clark kent)	\/wiki\/superman_(clark_kent)	secret identity	good characters	blue eyes	black hair	male characters	straight	living characters	2496.0	1986, october	1986.0
2	1458	green lantern (hal jordan)	\/wiki\/green_lantern_(hal_jordan)	secret identity	good characters	brown eyes	brown hair	male characters	straight	living characters	1565.0	1959, october	1959.0
3	1659	james gordon (new earth)	\/wiki\/james_gordon_(new_earth)	public identity	good characters	brown eyes	white hair	male characters	straight	living characters	1316.0	1987, february	1987.0
4	1576	richard grayson (new earth)	\/wiki\/richard_grayson_(new_earth)	secret identity	good characters	blue eyes	black hair	male characters	straight	living characters	1237.0	1940, april	1940.0
...	...	...	...	...	...	...	...	...	...	...	...	...	...
23267	657508	ru'ach (earth-616)	\/ru%27ach_(earth-616)	no dual identity	bad characters	green eyes	no hair	male characters	straight	living characters	NaN	NaN	NaN
23268	665474	thane (thanos' son) (earth-616)	\/thane_(thanos%27_son)_(earth-616)	no dual identity	good characters	blue eyes	bald	male characters	straight	living characters	NaN	NaN	NaN
23269	695217	tinkerer (skrull) (earth-616)	\/tinkerer_(skrull)_(earth-616)	secret identity	bad characters	black eyes	bald	male characters	straight	living characters	NaN	NaN	NaN
23270	708811	tk421 (spiderling) (earth-616)	\/tk421_(spiderling)_(earth-616)	secret identity	neutral characters	NaN	bald	male characters	straight	living characters	NaN	NaN	NaN
23271	673702	yologarch (earth-616)	\/yologarch_(earth-616)	NaN	bad characters	NaN	bald	NaN	straight	living characters	NaN	NaN	NaN
23272 rows × 13 columns
In [167]:
#How many characters in DC universe?
len(dc_data_df)
Out[167]:
6896
In [168]:
#How many characters in Marvel universe?
len(marvel_data_df)
Out[168]:
16376
In [169]:
#How many characters in each universe?
len(combined_hero_data)
Out[169]:
23272
In [170]:
#Gender in DC Universe
dc_gender_df = pd.read_csv('../Project_1/dc-wikia-data_csv.csv')
dc_gender = dc_gender_df['sex']
In [171]:
dc_gender
Out[171]:
0         male characters
1         male characters
2         male characters
3         male characters
4         male characters
              ...        
6891    female characters
6892      male characters
6893      male characters
6894      male characters
6895      male characters
Name: sex, Length: 6896, dtype: object
In [172]:
#Count the number of male, female, genderless, and transgender characters in DC Universe
dc_gender_count = dc_gender_df.groupby('sex')

dc_genders = dc_gender_count['sex'].count()

dc_genders
Out[172]:
sex
female characters         1967
genderless characters       20
male characters           4783
transgender characters       1
Name: sex, dtype: int64
In [173]:
#Chart showing breakdown of genders in DC Universe
dc_gender_count = dc_gender_count['sex'].value_counts()

bar_plot = dc_gender_count.plot.bar(color='tab:blue') 

plt.xlabel("Genders")
plt.ylabel("Count of genders")


plt.title("Genders Count in the DC Universe")
 
Out[173]:
Text(0.5, 1.0, 'Genders Count in the DC Universe')
In [174]:
marvel_gender_df = pd.read_csv('../Project_1/marvel-wikia-data_csv.csv')
marvel_gender = marvel_gender_df['sex']
In [175]:
marvel_gender
Out[175]:
0        male characters
1        male characters
2        male characters
3        male characters
4        male characters
              ...       
16371    male characters
16372    male characters
16373    male characters
16374    male characters
16375                NaN
Name: sex, Length: 16376, dtype: object
In [176]:
marvel_gender_df['sex'].value_counts()
Out[176]:
male characters           11638
female characters          3837
agender characters           45
genderfluid characters        2
Name: sex, dtype: int64
In [177]:
marvel_gender_count = marvel_gender_df['sex'].value_counts()


plt.xlabel("Genders")
plt.ylabel("Count of genders")

plt.title("Genders Count in the Marvel Universe")

bar_plot = marvel_gender_count.plot.bar()
In [178]:
#Chart showing breakdown of genders in Marvel Universe
marvel_gender_count.to_frame().plot.bar()

marvel_gender_count = marvel_gender_df['sex'].value_counts()


plt.xlabel("Genders")
plt.ylabel("Count of genders")

plt.title("Genders Count in the Marvel Universe")
 
Out[178]:
Text(0.5, 1.0, 'Genders Count in the Marvel Universe')
In [179]:
dc_eye_df = pd.read_csv('../Project_1/dc-wikia-data_csv.csv')
dc_eye = dc_eye_df['eye']
In [180]:
#Display breakdown of eye color in DC Universe
dc_eye_df['eye'].value_counts()
Out[180]:
blue eyes             1102
brown eyes             879
black eyes             412
green eyes             291
red eyes               208
white eyes             116
yellow eyes             86
photocellular eyes      48
grey eyes               40
hazel eyes              23
purple eyes             14
violet eyes             12
orange eyes             10
gold eyes                9
auburn hair              7
pink eyes                6
amber eyes               5
Name: eye, dtype: int64
In [181]:
eyes = ["Blue Eyes", "Brown Eyes", "Black Eyes", "Green Eyes", "Red Eyes", "White Eyes", "Yellow Eyes", 
          "Photocellular Eyes", "Grey Eyes", "Hazel Eyes", "Purple Eyes", "Violet Eyes", "Orange Eyes", "Gold Eyes", 
          "Auburn Eyes","Pink Eyes","Amber Eyes"]

# The values of each section of the pie chart
sizes = [1102, 879, 412, 291, 208, 116, 86, 48, 40, 23, 14, 12, 10, 9, 7, 6, 5]

# The colors of each section of the pie chart
colors = ["Blue", "Brown", "Black", "Green", "Red", "White", "Yellow", 
          "White", "Grey", "lightcoral", "Purple", "Violet", "Orange", "Gold", 
          "lightskyblue","Pink","crimson"]

# Tells matplotlib to separate the "Eyes" section from the others
explode = (0.5, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0)
In [182]:
#Pie Chart showing breakdown of genders in Mark Universe
dc_eye_pie = dc_eye_df["eye"].value_counts()
dc_eye_pie.plot.pie(autopct = "%1.1f%%")
plt.show()
In [197]:
labels = ["Blue Eyes", "Brown Eyes", "Black Eyes", "Green Eyes", "Red Eyes", "White Eyes", "Yellow Eyes", 
          "Photocellular Eyes", "Grey Eyes", "Hazel Eyes", "Purple Eyes", "Violet Eyes", "Orange Eyes", "Gold Eyes", 
          "Auburn Eyes","Pink Eyes","Amber Eyes"]
sizes = [1102, 879, 412, 291, 208, 116, 86, 48, 40, 23, 14, 12, 10, 9, 7, 6, 5]
plot = dc_eye.plot.pie(y='Total Count', autopct="%1.1f%%")
plt.ylabel('eye')
plt.title("Eye Color in DC Universe")
plt.show()
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
~\AppData\Local\Temp\ipykernel_25184\1399132646.py in <module>
      3           "Auburn Eyes","Pink Eyes","Amber Eyes"]
      4 sizes = [1102, 879, 412, 291, 208, 116, 86, 48, 40, 23, 14, 12, 10, 9, 7, 6, 5]
----> 5 plot = dc_eye.plot.pie(y='Total Count', autopct="%1.1f%%")
      6 plt.ylabel('eye')
      7 plt.title("Eye Color in DC Universe")

~\anaconda3\lib\site-packages\pandas\plotting\_core.py in pie(self, **kwargs)
   1582         ):
   1583             raise ValueError("pie requires either y column or 'subplots=True'")
-> 1584         return self(kind="pie", **kwargs)
   1585 
   1586     def scatter(self, x, y, s=None, c=None, **kwargs):

~\anaconda3\lib\site-packages\pandas\plotting\_core.py in __call__(self, *args, **kwargs)
    970                     data.columns = label_name
    971 
--> 972         return plot_backend.plot(data, kind=kind, **kwargs)
    973 
    974     __call__.__doc__ = __doc__

~\anaconda3\lib\site-packages\pandas\plotting\_matplotlib\__init__.py in plot(data, kind, **kwargs)
     68                 ax = plt.gca()
     69             kwargs["ax"] = getattr(ax, "left_ax", ax)
---> 70     plot_obj = PLOT_CLASSES[kind](data, **kwargs)
     71     plot_obj.generate()
     72     plot_obj.draw()

~\anaconda3\lib\site-packages\pandas\plotting\_matplotlib\core.py in __init__(self, data, kind, **kwargs)
   1624     def __init__(self, data, kind=None, **kwargs):
   1625         data = data.fillna(value=0)
-> 1626         if (data < 0).any().any():
   1627             raise ValueError(f"{self._kind} plot doesn't allow negative values")
   1628         MPLPlot.__init__(self, data, kind=kind, **kwargs)

~\anaconda3\lib\site-packages\pandas\core\ops\common.py in new_method(self, other)
     68         other = item_from_zerodim(other)
     69 
---> 70         return method(self, other)
     71 
     72     return new_method

~\anaconda3\lib\site-packages\pandas\core\arraylike.py in __lt__(self, other)
     46     @unpack_zerodim_and_defer("__lt__")
     47     def __lt__(self, other):
---> 48         return self._cmp_method(other, operator.lt)
     49 
     50     @unpack_zerodim_and_defer("__le__")

~\anaconda3\lib\site-packages\pandas\core\series.py in _cmp_method(self, other, op)
   5621 
   5622         with np.errstate(all="ignore"):
-> 5623             res_values = ops.comparison_op(lvalues, rvalues, op)
   5624 
   5625         return self._construct_result(res_values, name=res_name)

~\anaconda3\lib\site-packages\pandas\core\ops\array_ops.py in comparison_op(left, right, op)
    281 
    282     elif is_object_dtype(lvalues.dtype) or isinstance(rvalues, str):
--> 283         res_values = comp_method_OBJECT_ARRAY(op, lvalues, rvalues)
    284 
    285     else:

~\anaconda3\lib\site-packages\pandas\core\ops\array_ops.py in comp_method_OBJECT_ARRAY(op, x, y)
     71         result = libops.vec_compare(x.ravel(), y.ravel(), op)
     72     else:
---> 73         result = libops.scalar_compare(x.ravel(), y, op)
     74     return result.reshape(x.shape)
     75 

~\anaconda3\lib\site-packages\pandas\_libs\ops.pyx in pandas._libs.ops.scalar_compare()

TypeError: '<' not supported between instances of 'str' and 'int'
In [184]:
marvel_eye_df = pd.read_csv('../Project_1/marvel-wikia-data_csv.csv')
marvel_eye = marvel_eye_df['eye']
In [185]:
#Display breakdown of eye color in Marvel Universe
marvel_eye_df['eye'].value_counts()
Out[185]:
blue eyes          1962
brown eyes         1924
green eyes          613
black eyes          555
red eyes            508
white eyes          400
yellow eyes         256
grey eyes            95
hazel eyes           76
variable eyes        49
purple eyes          31
orange eyes          25
pink eyes            21
one eye              21
gold eyes            14
silver eyes          12
violet eyes          11
amber eyes           10
multiple eyes         7
no eyes               7
yellow eyeballs       6
black eyeballs        3
magenta eyes          2
compound eyes         1
Name: eye, dtype: int64
In [186]:
eyes = ["Blue Eyes", "Brown Eyes", "Green Eyes", "Black Eyes", "Red Eyes", "White Eyes", "Yellow Eyes", 
          "Grey Eyes", "Hazel Eyes", "Variable Eyes", "Purple Eyes", "Orange Eyes", "Pink Eyes", 
          "One Eye","Gold Eyes","Silver Eyes", "Violet Eye","Amber Eyes","Multiple Eyes",  
        "No Eyes","Yellow Eyesballs","Black Eyesballs", "Magenta Eye","Compound Eyes"]

# The values of each section of the pie chart
sizes = [1962, 1924, 613, 555, 508, 400, 256, 95, 76, 49, 31, 25, 21, 21, 14, 12, 11, 10, 7, 7, 6, 3, 2, 1]

# The colors of each section of the pie chart
colors = ["Blue", "Brown", "Green", "Black", "Red", "White", "Yellow", 
          "Grey", "lightcoral", "yellowgreen", "Purple", "Orange", "Pink", 
          "beige","Gold","Silver", "Violet","crimson","lightblue",  
        "lightbrow","lightyellow","lightblack", "Magenta","lightgrey"]

# Tells matplotlib to separate the "Eyes" section from the others
explode = (0.5, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0)
In [187]:
#Pie Chart showing breakdown of genders in Marvel Universe
plt.title("Eye Colors in Marvel Universe")
plt.pie(sizes, explode=explode, labels=eyes, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=25)
plt.axis("equal")

plt.show()
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
~\AppData\Local\Temp\ipykernel_25184\3007183459.py in <module>
      1 #Pie Chart showing breakdown of genders in Marvel Universe
      2 plt.title("Eye Colors in Marvel Universe")
----> 3 plt.pie(sizes, explode=explode, labels=eyes, colors=colors,
      4         autopct="%1.1f%%", shadow=True, startangle=25)
      5 plt.axis("equal")

~\anaconda3\lib\site-packages\matplotlib\pyplot.py in pie(x, explode, labels, colors, autopct, pctdistance, shadow, labeldistance, startangle, radius, counterclock, wedgeprops, textprops, center, frame, rotatelabels, normalize, data)
   2754         textprops=None, center=(0, 0), frame=False,
   2755         rotatelabels=False, *, normalize=True, data=None):
-> 2756     return gca().pie(
   2757         x, explode=explode, labels=labels, colors=colors,
   2758         autopct=autopct, pctdistance=pctdistance, shadow=shadow,

~\anaconda3\lib\site-packages\matplotlib\__init__.py in inner(ax, data, *args, **kwargs)
   1410     def inner(ax, *args, data=None, **kwargs):
   1411         if data is None:
-> 1412             return func(ax, *map(sanitize_sequence, args), **kwargs)
   1413 
   1414         bound = new_sig.bind(ax, *args, **kwargs)

~\anaconda3\lib\site-packages\matplotlib\axes\_axes.py in pie(self, x, explode, labels, colors, autopct, pctdistance, shadow, labeldistance, startangle, radius, counterclock, wedgeprops, textprops, center, frame, rotatelabels, normalize)
   3090             y += expl * math.sin(thetam)
   3091 
-> 3092             w = mpatches.Wedge((x, y), radius, 360. * min(theta1, theta2),
   3093                                360. * max(theta1, theta2),
   3094                                facecolor=get_next_color(),

~\anaconda3\lib\site-packages\matplotlib\patches.py in __init__(self, center, r, theta1, theta2, width, **kwargs)
   1157         %(Patch:kwdoc)s
   1158         """
-> 1159         super().__init__(**kwargs)
   1160         self.center = center
   1161         self.r, self.width = r, width

~\anaconda3\lib\site-packages\matplotlib\patches.py in __init__(self, edgecolor, facecolor, color, linewidth, linestyle, antialiased, hatch, fill, capstyle, joinstyle, **kwargs)
     97         else:
     98             self.set_edgecolor(edgecolor)
---> 99             self.set_facecolor(facecolor)
    100         # unscaled dashes.  Needed to scale dash patterns by lw
    101         self._us_dashes = None

~\anaconda3\lib\site-packages\matplotlib\patches.py in set_facecolor(self, color)
    371         """
    372         self._original_facecolor = color
--> 373         self._set_facecolor(color)
    374 
    375     def set_color(self, c):

~\anaconda3\lib\site-packages\matplotlib\patches.py in _set_facecolor(self, color)
    359             color = mpl.rcParams['patch.facecolor']
    360         alpha = self._alpha if self._fill else 0
--> 361         self._facecolor = colors.to_rgba(color, alpha)
    362         self.stale = True
    363 

~\anaconda3\lib\site-packages\matplotlib\colors.py in to_rgba(c, alpha)
    185         rgba = None
    186     if rgba is None:  # Suppress exception chaining of cache lookup failure.
--> 187         rgba = _to_rgba_no_colorcycle(c, alpha)
    188         try:
    189             _colors_full_map.cache[c, alpha] = rgba

~\anaconda3\lib\site-packages\matplotlib\colors.py in _to_rgba_no_colorcycle(c, alpha)
    260                     f"Value must be within 0-1 range")
    261             return c, c, c, alpha if alpha is not None else 1.
--> 262         raise ValueError(f"Invalid RGBA argument: {orig_c!r}")
    263     # turn 2-D array into 1-D array
    264     if isinstance(c, np.ndarray):

ValueError: Invalid RGBA argument: 'lightbrow'
In [188]:
dc_orientation_df = pd.read_csv('../Project_1/dc-wikia-data_csv.csv')
dc_orientation = dc_orientation_df['gsm']
In [189]:
#Display breakdown of sexual orientation in DC Universe
dc_orientation_df['gsm'].value_counts()
Out[189]:
straight                 6832
homosexual characters      54
bisexual characters        10
Name: gsm, dtype: int64
In [190]:
dc_orientation_count = dc_orientation_df.groupby('gsm')

dc_orientation = dc_orientation_count['gsm'].count()

dc_orientation
Out[190]:
gsm
bisexual characters        10
homosexual characters      54
straight                 6832
Name: gsm, dtype: int64
In [191]:
dc_orientation_count = dc_orientation_count['gsm'].value_counts()

bar_plot = dc_orientation_count.plot.bar(color='tab:blue') 

plt.xlabel("Genders")
plt.ylabel("Count of genders")


plt.title("Sexual Orientation Count in the DC Universe")
Out[191]:
Text(0.5, 1.0, 'Sexual Orientation Count in the DC Universe')
In [192]:
marvel_orientation_df = pd.read_csv('../Project_1/marvel-wikia-data_csv.csv')
marvel_orientation = marvel_orientation_df['gsm']
In [193]:
marvel_orientation_df['gsm'].value_counts()
Out[193]:
straight                  16286
homosexual characters        66
bisexual characters          19
transgender characters        2
transvestites                 1
pansexual characters          1
genderfluid characters        1
Name: gsm, dtype: int64
In [194]:
marvel_orientation_count = marvel_orientation_df.groupby('gsm')

marvel_orientation = marvel_orientation_count['gsm'].count()

marvel_orientation
Out[194]:
gsm
bisexual characters          19
genderfluid characters        1
homosexual characters        66
pansexual characters          1
straight                  16286
transgender characters        2
transvestites                 1
Name: gsm, dtype: int64
In [195]:
marvel_orientation_count = marvel_orientation_count['gsm'].value_counts()

bar_plot = marvel_orientation_count.plot.bar(color='tab:blue') 

plt.xlabel("Genders")
plt.ylabel("Count of genders")


plt.title("Sexual Orientation Count in the Marvel Universe")
Out[195]:
Text(0.5, 1.0, 'Sexual Orientation Count in the Marvel Universe')

import pandas as pd
import matplotlib.pyplot as plt
In [253]:
movie_data = pd.read_csv("MARVELvsDC.csv")
movie_data
Out[253]:
	Movie Titles	Company	IMDB	Metascore	Minutes	Release	Budget	Opening Weekend USA	Gross USA	Gross Worldwide
1	Iron Man	Marvel	7.9	79	126	2008	140000000	98618668	318604126	585366247
2	The Incredible Hulk	Marvel	6.7	61	112†	2008	150000000	55414050	134806913	263427551
3	Iron Man 2	Marvel	7.0	57	124†	2010	200000000	128122480	312433331	623933331
4	Thor	Marvel	7.0	57	115	2011	150000000†	65723338	181030624	449326618
5	Captain America: The First Avenger	Marvel	6.9	66	124	2011	140000000	65058524	176654505	370569774
6	The Avengers	Marvel	8.0	69	143	2012	220000000	207438708	623357910	1518812988
7	Iron Man Three	Marvel	7.2	62	130	2013	200000000†	174144585	409013994	1214811252
8	Thor: The Dark World	Marvel	6.9	54	112	2013	170000000	85737841	206362140	644783140
9	Captain America: The Winter Soldier	Marvel	7.7	70	136	2014	170000000	95023721	259766572	714421503
10	Guardians of the Galaxy	Marvel	8.0	76	121	2014	170000000	94320883	333176600	772776600
11	Avengers: Age of Ultron†	Marvel	7.3	66	141	2015	250000000	191271109	459005868	1402805868
12	Ant-Man	Marvel	7.3	64	117	2015	130000000	57225526	180202163	519311965
13	Captain America: Civil War	Marvel	7.8	75	147	2016	250000000	179139142	408084349	1153296293
14	Doctor Strange	Marvel	7.5	72	115	2016	165000000	85058311	232641920	677718395
15	Guardians of the Galaxy Vol. 2	Marvel	7.6	67	136	2017	200000000	146510104	389813101	863756051
16	Spider-Man: Homecoming	Marvel	7.4	73	133	2017	175000000†	117027503	334201140	880166924
17	Thor:Ragnarok	Marvel	7.9	74	130	2017	180000000	122744989	315058289	853977126
18	Black Panther	Marvel	7.3	88	134	2018	200000000	202003951	700059566	1346913161
19	Avengers: Infinity War	Marvel	8.5	68	149	2018	321000000†	257698183	678815482	2048359754
20	Ant-Man and the Wasp	Marvel	7.1	70	118	2018	162000000	75812205	216648740	622674139
21	Captain Marve	Marvel	6.9	64	123	2019	175000000†	153433423	426829839	1128274794
22	Avengers: Endgame	Marvel	8.5	78	181	2019	356000000	357115007	858373000	2797800564
23	Spider-Man: Far from Home	Marvel	7.6	69	129	2019	160000000	92579212	390532085	1131927996
24	Catwoman	DC	3.3	27	104	2004	100000000	16728411	40202379	82102379
25	Batman Begins	DC	8.2	70	140	2005	150000000	48745440	206852432	373413297
26	Superman Returns	DC	6.0	72	154	2006	270000000	52535096	200081192	391081192
27	The Dark Knight	DC	9.0	84	152	2008	185000000	158411483	535234033	1004934033
28	Watchmen	DC	7.6	56	162	2009	130000000	55214334	107509799	185258983
29	Jonah Hex†	DC	4.7	33	81	2010	47000000†	5379365	10547117	10903312
30	Green Lantern	DC	5.5	39	114	2011	200000000	53174303	116601172	219851172
31	The Dark Knight Rises	DC	8.4	78	164	2012	250000000	160887295	448139099	1081041287
32	Man of Steel	DC	7.1	55	143	2013	225000000	116619362	291045518	668045518
33	Batman v Superman: Dawn of Justice	DC	6.5	44	151	2016	250000000	166007347	330360194	873634919
34	Suicide Squad†	DC	6.0	40	123	2016	175000000	133682248	325100054	746846894
35	Wonder Woman	DC	7.4	76	141	2017	149000000	103251471	412563408	821847012
36	Justice League	DC	6.4	45	120	2017	300000000	93842239	229024295	657924295
37	Aquaman	DC	7.0	55	143	2018	160000000	67873522	335061807	1148161807
38	Shazam!	DC	7.1	71	132	2019	100000000	53505326	140371656	364571656
39	Joker	DC	8.7	59	122	2019	55000000†	96202337	333204580	1060504580
In [254]:
#marvel movies
Marvel_data = movie_data[movie_data['Company'] == "Marvel"]
Marvel_data
Out[254]:
	Movie Titles	Company	IMDB	Metascore	Minutes	Release	Budget	Opening Weekend USA	Gross USA	Gross Worldwide
1	Iron Man	Marvel	7.9	79	126	2008	140000000	98618668	318604126	585366247
2	The Incredible Hulk	Marvel	6.7	61	112†	2008	150000000	55414050	134806913	263427551
3	Iron Man 2	Marvel	7.0	57	124†	2010	200000000	128122480	312433331	623933331
4	Thor	Marvel	7.0	57	115	2011	150000000†	65723338	181030624	449326618
5	Captain America: The First Avenger	Marvel	6.9	66	124	2011	140000000	65058524	176654505	370569774
6	The Avengers	Marvel	8.0	69	143	2012	220000000	207438708	623357910	1518812988
7	Iron Man Three	Marvel	7.2	62	130	2013	200000000†	174144585	409013994	1214811252
8	Thor: The Dark World	Marvel	6.9	54	112	2013	170000000	85737841	206362140	644783140
9	Captain America: The Winter Soldier	Marvel	7.7	70	136	2014	170000000	95023721	259766572	714421503
10	Guardians of the Galaxy	Marvel	8.0	76	121	2014	170000000	94320883	333176600	772776600
11	Avengers: Age of Ultron†	Marvel	7.3	66	141	2015	250000000	191271109	459005868	1402805868
12	Ant-Man	Marvel	7.3	64	117	2015	130000000	57225526	180202163	519311965
13	Captain America: Civil War	Marvel	7.8	75	147	2016	250000000	179139142	408084349	1153296293
14	Doctor Strange	Marvel	7.5	72	115	2016	165000000	85058311	232641920	677718395
15	Guardians of the Galaxy Vol. 2	Marvel	7.6	67	136	2017	200000000	146510104	389813101	863756051
16	Spider-Man: Homecoming	Marvel	7.4	73	133	2017	175000000†	117027503	334201140	880166924
17	Thor:Ragnarok	Marvel	7.9	74	130	2017	180000000	122744989	315058289	853977126
18	Black Panther	Marvel	7.3	88	134	2018	200000000	202003951	700059566	1346913161
19	Avengers: Infinity War	Marvel	8.5	68	149	2018	321000000†	257698183	678815482	2048359754
20	Ant-Man and the Wasp	Marvel	7.1	70	118	2018	162000000	75812205	216648740	622674139
21	Captain Marve	Marvel	6.9	64	123	2019	175000000†	153433423	426829839	1128274794
22	Avengers: Endgame	Marvel	8.5	78	181	2019	356000000	357115007	858373000	2797800564
23	Spider-Man: Far from Home	Marvel	7.6	69	129	2019	160000000	92579212	390532085	1131927996
In [255]:
dc_data = movie_data[movie_data['Company'] == "DC"]
dc_data
Out[255]:
	Movie Titles	Company	IMDB	Metascore	Minutes	Release	Budget	Opening Weekend USA	Gross USA	Gross Worldwide
24	Catwoman	DC	3.3	27	104	2004	100000000	16728411	40202379	82102379
25	Batman Begins	DC	8.2	70	140	2005	150000000	48745440	206852432	373413297
26	Superman Returns	DC	6.0	72	154	2006	270000000	52535096	200081192	391081192
27	The Dark Knight	DC	9.0	84	152	2008	185000000	158411483	535234033	1004934033
28	Watchmen	DC	7.6	56	162	2009	130000000	55214334	107509799	185258983
29	Jonah Hex†	DC	4.7	33	81	2010	47000000†	5379365	10547117	10903312
30	Green Lantern	DC	5.5	39	114	2011	200000000	53174303	116601172	219851172
31	The Dark Knight Rises	DC	8.4	78	164	2012	250000000	160887295	448139099	1081041287
32	Man of Steel	DC	7.1	55	143	2013	225000000	116619362	291045518	668045518
33	Batman v Superman: Dawn of Justice	DC	6.5	44	151	2016	250000000	166007347	330360194	873634919
34	Suicide Squad†	DC	6.0	40	123	2016	175000000	133682248	325100054	746846894
35	Wonder Woman	DC	7.4	76	141	2017	149000000	103251471	412563408	821847012
36	Justice League	DC	6.4	45	120	2017	300000000	93842239	229024295	657924295
37	Aquaman	DC	7.0	55	143	2018	160000000	67873522	335061807	1148161807
38	Shazam!	DC	7.1	71	132	2019	100000000	53505326	140371656	364571656
39	Joker	DC	8.7	59	122	2019	55000000†	96202337	333204580	1060504580
In [256]:
#IMDB rating
Imdb_data = movie_data.sort_values(by=['IMDB'], ascending=[False])
Imdb_data
Out[256]:
	Movie Titles	Company	IMDB	Metascore	Minutes	Release	Budget	Opening Weekend USA	Gross USA	Gross Worldwide
27	The Dark Knight	DC	9.0	84	152	2008	185000000	158411483	535234033	1004934033
39	Joker	DC	8.7	59	122	2019	55000000†	96202337	333204580	1060504580
22	Avengers: Endgame	Marvel	8.5	78	181	2019	356000000	357115007	858373000	2797800564
19	Avengers: Infinity War	Marvel	8.5	68	149	2018	321000000†	257698183	678815482	2048359754
31	The Dark Knight Rises	DC	8.4	78	164	2012	250000000	160887295	448139099	1081041287
25	Batman Begins	DC	8.2	70	140	2005	150000000	48745440	206852432	373413297
10	Guardians of the Galaxy	Marvel	8.0	76	121	2014	170000000	94320883	333176600	772776600
6	The Avengers	Marvel	8.0	69	143	2012	220000000	207438708	623357910	1518812988
17	Thor:Ragnarok	Marvel	7.9	74	130	2017	180000000	122744989	315058289	853977126
1	Iron Man	Marvel	7.9	79	126	2008	140000000	98618668	318604126	585366247
13	Captain America: Civil War	Marvel	7.8	75	147	2016	250000000	179139142	408084349	1153296293
9	Captain America: The Winter Soldier	Marvel	7.7	70	136	2014	170000000	95023721	259766572	714421503
15	Guardians of the Galaxy Vol. 2	Marvel	7.6	67	136	2017	200000000	146510104	389813101	863756051
23	Spider-Man: Far from Home	Marvel	7.6	69	129	2019	160000000	92579212	390532085	1131927996
28	Watchmen	DC	7.6	56	162	2009	130000000	55214334	107509799	185258983
14	Doctor Strange	Marvel	7.5	72	115	2016	165000000	85058311	232641920	677718395
16	Spider-Man: Homecoming	Marvel	7.4	73	133	2017	175000000†	117027503	334201140	880166924
35	Wonder Woman	DC	7.4	76	141	2017	149000000	103251471	412563408	821847012
11	Avengers: Age of Ultron†	Marvel	7.3	66	141	2015	250000000	191271109	459005868	1402805868
12	Ant-Man	Marvel	7.3	64	117	2015	130000000	57225526	180202163	519311965
18	Black Panther	Marvel	7.3	88	134	2018	200000000	202003951	700059566	1346913161
7	Iron Man Three	Marvel	7.2	62	130	2013	200000000†	174144585	409013994	1214811252
38	Shazam!	DC	7.1	71	132	2019	100000000	53505326	140371656	364571656
32	Man of Steel	DC	7.1	55	143	2013	225000000	116619362	291045518	668045518
20	Ant-Man and the Wasp	Marvel	7.1	70	118	2018	162000000	75812205	216648740	622674139
4	Thor	Marvel	7.0	57	115	2011	150000000†	65723338	181030624	449326618
3	Iron Man 2	Marvel	7.0	57	124†	2010	200000000	128122480	312433331	623933331
37	Aquaman	DC	7.0	55	143	2018	160000000	67873522	335061807	1148161807
21	Captain Marve	Marvel	6.9	64	123	2019	175000000†	153433423	426829839	1128274794
8	Thor: The Dark World	Marvel	6.9	54	112	2013	170000000	85737841	206362140	644783140
5	Captain America: The First Avenger	Marvel	6.9	66	124	2011	140000000	65058524	176654505	370569774
2	The Incredible Hulk	Marvel	6.7	61	112†	2008	150000000	55414050	134806913	263427551
33	Batman v Superman: Dawn of Justice	DC	6.5	44	151	2016	250000000	166007347	330360194	873634919
36	Justice League	DC	6.4	45	120	2017	300000000	93842239	229024295	657924295
26	Superman Returns	DC	6.0	72	154	2006	270000000	52535096	200081192	391081192
34	Suicide Squad†	DC	6.0	40	123	2016	175000000	133682248	325100054	746846894
30	Green Lantern	DC	5.5	39	114	2011	200000000	53174303	116601172	219851172
29	Jonah Hex†	DC	4.7	33	81	2010	47000000†	5379365	10547117	10903312
24	Catwoman	DC	3.3	27	104	2004	100000000	16728411	40202379	82102379
In [257]:
#Meta score rating
meta_data = movie_data.sort_values(by=['Metascore'], ascending=[False])
meta_data
Out[257]:
	Movie Titles	Company	IMDB	Metascore	Minutes	Release	Budget	Opening Weekend USA	Gross USA	Gross Worldwide
18	Black Panther	Marvel	7.3	88	134	2018	200000000	202003951	700059566	1346913161
27	The Dark Knight	DC	9.0	84	152	2008	185000000	158411483	535234033	1004934033
1	Iron Man	Marvel	7.9	79	126	2008	140000000	98618668	318604126	585366247
31	The Dark Knight Rises	DC	8.4	78	164	2012	250000000	160887295	448139099	1081041287
22	Avengers: Endgame	Marvel	8.5	78	181	2019	356000000	357115007	858373000	2797800564
35	Wonder Woman	DC	7.4	76	141	2017	149000000	103251471	412563408	821847012
10	Guardians of the Galaxy	Marvel	8.0	76	121	2014	170000000	94320883	333176600	772776600
13	Captain America: Civil War	Marvel	7.8	75	147	2016	250000000	179139142	408084349	1153296293
17	Thor:Ragnarok	Marvel	7.9	74	130	2017	180000000	122744989	315058289	853977126
16	Spider-Man: Homecoming	Marvel	7.4	73	133	2017	175000000†	117027503	334201140	880166924
26	Superman Returns	DC	6.0	72	154	2006	270000000	52535096	200081192	391081192
14	Doctor Strange	Marvel	7.5	72	115	2016	165000000	85058311	232641920	677718395
38	Shazam!	DC	7.1	71	132	2019	100000000	53505326	140371656	364571656
25	Batman Begins	DC	8.2	70	140	2005	150000000	48745440	206852432	373413297
20	Ant-Man and the Wasp	Marvel	7.1	70	118	2018	162000000	75812205	216648740	622674139
9	Captain America: The Winter Soldier	Marvel	7.7	70	136	2014	170000000	95023721	259766572	714421503
6	The Avengers	Marvel	8.0	69	143	2012	220000000	207438708	623357910	1518812988
23	Spider-Man: Far from Home	Marvel	7.6	69	129	2019	160000000	92579212	390532085	1131927996
19	Avengers: Infinity War	Marvel	8.5	68	149	2018	321000000†	257698183	678815482	2048359754
15	Guardians of the Galaxy Vol. 2	Marvel	7.6	67	136	2017	200000000	146510104	389813101	863756051
11	Avengers: Age of Ultron†	Marvel	7.3	66	141	2015	250000000	191271109	459005868	1402805868
5	Captain America: The First Avenger	Marvel	6.9	66	124	2011	140000000	65058524	176654505	370569774
21	Captain Marve	Marvel	6.9	64	123	2019	175000000†	153433423	426829839	1128274794
12	Ant-Man	Marvel	7.3	64	117	2015	130000000	57225526	180202163	519311965
7	Iron Man Three	Marvel	7.2	62	130	2013	200000000†	174144585	409013994	1214811252
2	The Incredible Hulk	Marvel	6.7	61	112†	2008	150000000	55414050	134806913	263427551
39	Joker	DC	8.7	59	122	2019	55000000†	96202337	333204580	1060504580
4	Thor	Marvel	7.0	57	115	2011	150000000†	65723338	181030624	449326618
3	Iron Man 2	Marvel	7.0	57	124†	2010	200000000	128122480	312433331	623933331
28	Watchmen	DC	7.6	56	162	2009	130000000	55214334	107509799	185258983
32	Man of Steel	DC	7.1	55	143	2013	225000000	116619362	291045518	668045518
37	Aquaman	DC	7.0	55	143	2018	160000000	67873522	335061807	1148161807
8	Thor: The Dark World	Marvel	6.9	54	112	2013	170000000	85737841	206362140	644783140
36	Justice League	DC	6.4	45	120	2017	300000000	93842239	229024295	657924295
33	Batman v Superman: Dawn of Justice	DC	6.5	44	151	2016	250000000	166007347	330360194	873634919
34	Suicide Squad†	DC	6.0	40	123	2016	175000000	133682248	325100054	746846894
30	Green Lantern	DC	5.5	39	114	2011	200000000	53174303	116601172	219851172
29	Jonah Hex†	DC	4.7	33	81	2010	47000000†	5379365	10547117	10903312
24	Catwoman	DC	3.3	27	104	2004	100000000	16728411	40202379	82102379
In [272]:
grouped = movie_data.groupby('Company').mean()

fig, ax = plt.subplots(1, 2, figsize=(10, 5))
ax[0].bar(grouped.index, grouped['IMDB'], color='red')
ax[0].set_title('Average IMDB Score')

ax[1].bar(grouped.index, grouped['Metascore'])
ax[1].set_title('Average MetaScore')

plt.show()
 
In [259]:
# IMDB scores
movie_data["IMDB"] = pd.to_numeric(movie_data["IMDB"], errors='coerce')
grouped = movie_data.groupby("Company").mean()

plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1)
plt.pie(grouped["IMDB"], labels=grouped.index, autopct='%1.1f%%')
plt.title("IMDB scores for Marvel and DC")

# Metascores
movie_data["Metascore"] = pd.to_numeric(movie_data["Metascore"], errors='coerce')
grouped = movie_data.groupby("Company").mean()

plt.subplot(1, 2, 2)
plt.pie(grouped["Metascore"], labels=grouped.index, autopct='%1.1f%%')
plt.title("Metascores for Marvel and DC")

plt.show()
 
In [273]:
grouped = movie_data.groupby('Company').mean()

fig, ax = plt.subplots(1, 2, figsize=(10, 5))
ax[0].bar(grouped.index, grouped['Gross USA'],color='red')
ax[0].set_title('Gross USA')

ax[1].bar(grouped.index, grouped['Gross Worldwide'])
ax[1].set_title('Gross Worldwide')

plt.show()
 
In [270]:
# Gross USA scores
movie_data["Gross USA"] = pd.to_numeric(movie_data["Gross USA"], errors='coerce')
grouped = movie_data.groupby("Company").mean()

plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1)
plt.pie(grouped["Gross USA"], labels=grouped.index, autopct='%1.1f%%')
plt.title("Gross USA")

# Gross Worldwide
movie_data["Gross Worldwide"] = pd.to_numeric(movie_data["Gross Worldwide"], errors='coerce')
grouped = movie_data.groupby("Company").mean()

plt.subplot(1, 2, 2)
plt.pie(grouped["Gross Worldwide"], labels=grouped.index, autopct='%1.1f%%')
plt.title("Gross Worldwide")

plt.show()
 
%matplotlib notebook
In [1]:
import pandas as pd
import matplotlib.pyplot as plt
from matplotlib import lines
from matplotlib import patches
from matplotlib.patheffects import withStroke
import scipy.stats as st
import numpy as np
In [2]:
# Character wealth CSV
character_wealth_df = pd.read_csv("character_wealth.csv")
character_wealth_df
Out[2]:
	Name	Alter_ego	Franchise	Type	Net_worth	Income_source	Entity_name	Entity_type
0	Aquaman	Arthur Curry	DC	Hero	$150,000,000,000,000	Monarch	Atlantis	Kingdom
1	Black Panther	T'Challa	Marvel	Hero	$90,700,000,000,000	Monarch	Kingdom of Wakanda	Kingdom
2	Namor	Namor McKenzie	Marvel	Hero	$260,000,000,000	Entrepreneur	Atlantis	Kingdom
3	Sunspot	Roberto da Costa	Marvel	Villain	$125,000,000,000	Inheritance	NaN	NaN
4	Iron Man	Tony Stark	Marvel	Hero	$100,000,000,000	Entrepreneur	Stark Industries	Multinational Conglomerate
5	Batman	Bruce Wayne	DC	Hero	$80,000,000,000	Inheritance	Wayne Enterprises	Multinational Conglomerate
6	Lex Luthor	Alexander Luthor	DC	Villain	$75,000,000,000	Entrepreneur	LexCorp	Multinational Conglomerate
7	Doctor Doom	Victor von Doom	Marvel	Villain	$35,000,000,000	Monarch	Latveria	Kingdom
8	Kingpin	Wilson Fisk	Marvel	Villain	$30,000,000,000	Entrepreneur	NaN	NaN
9	Black Adam	Theo Ramses Djoser Teth-Adam	DC	Villain	$12,000,000,000	Monarch	Khandaq	Kingdom
10	Ozymandias	Adrian Veidt	DC	Villain	$7,000,000,000	Entrepreneur	Veidt Enterprises	Multinational Conglomerate
11	Green Arrow	Oliver Queen	DC	Hero	$7,000,000,000	Inheritance	Queen Consolidated	Multinational Conglomerate
12	Green Goblin	Noram Osborn	Marvel	Villain	$5,000,000,000	Entrepreneur	Oscorp Industries	Multinational Conglomerate
13	Iron Fist	Daniel Rand	Marvel	Hero	$5,000,000,000	Inheritance	Rand Enterprises	Multinational Conglomerate
14	Archangel	Warren Worthington III	Marvel	Hero	$5,000,000,000	Inheritance	Worthington Industries	Multinational Conglomerate
15	Blue Beetle	Ted Kord	DC	Hero	$5,000,000,000	Inheritance	Kord Enterprises	Multinational Conglomerate
16	Nighthawk	Kyle Richmond	Marvel	Villain	$5,000,000,000	Inheritance	Richmond Enterprises	Multinational Conglomerate
17	Mister Fantastic	Reed Richards	Marvel	Hero	$5,000,000,000	Entrepreneur	Fantastic Four Inc	NaN
18	Simon Stagg	Simon Stagg	DC	Villain	$4,000,000,000	Entrepreneur	Stagg Industries	Multinational Conglomerate
19	Crystal	Crystalia Amaquelin	Marvel	Hero	$4,000,000,000	Inheritance	NaN	NaN
20	Professor X	Charles Xavier	Marvel	Hero	$3,500,000,000	Inheritance	NaN	NaN
21	White Queen	Emma Frost	Marvel	Villain	$3,000,000,000	Inheritance	Frost International	Export and Trading
22	Black Bolt	Blackagar Boltagon	Marvel	Hero	$2,500,000,000	Self-made	Inhumans of Attilan	NaN
23	Moon Knight	Marc Spector	Marvel	Hero	$2,300,000,000	Investments	NaN	NaN
24	Silver Sable	Silvija Sablinova	Marvel	Hero	$2,100,000,000	Self-made	Silver Sable International	Mercenary Corporation
25	Spiderman	Peter Parker	Marvel	Hero	$2,000,000,000	Entrepreneur	Parker Industries	Tech Conglomerate
26	Vandal Savage	Vandar Adg	DC	Villain	$2,000,000,000	Self-made	NaN	NaN
27	Nightwing	Dick Grayson	DC	Hero	$1,000,000,000	Inheritance	NaN	NaN
28	The Wasp	Janet van Dyne	Marvel	Hero	$1,000,000,000	Self-made	NaN	NaN
29	Mr. Terrific	Michael Holt	DC	Hero	$1,000,000,000	Entrepreneur	NaN	NaN
30	Maxwell Lord	Maxwell Lord	DC	Villain	$1,000,000,000	Entrepreneur	Black Gold Cooperative	Oil and Gas
31	Ra's Al Ghul	Ra's Al Ghul	DC	Villain	$1,000,000,000	Self-made	NaN	NaN
32	Michael Holt	Michael Holt	Marvel	Hero	$1,000,000,000	Entrepreneur	NaN	NaN
33	Star Sapphire	Carol Ferris	DC	Hero	$1,000,000,000	Inheritance	NaN	NaN
34	Power Girl	Kara Zor-L	DC	Hero	$1,000,000,000	Entrepreneur	NaN	NaN
35	Medusa	Medusalith Amaquelin-Boltagon	Marvel	Villain	$1,000,000,000	Monarch	Inhumans of Attilan	NaN
36	Magneto	Erik Lehnsherr	Marvel	Villain	$900,000,000	Self-made	NaN	NaN
In [3]:
# Show richest hero
hero_options = ["Type", "Hero"]
richest_hero = character_wealth_df[character_wealth_df["Type"].isin(hero_options)]
richest_hero
Out[3]:
	Name	Alter_ego	Franchise	Type	Net_worth	Income_source	Entity_name	Entity_type
0	Aquaman	Arthur Curry	DC	Hero	$150,000,000,000,000	Monarch	Atlantis	Kingdom
1	Black Panther	T'Challa	Marvel	Hero	$90,700,000,000,000	Monarch	Kingdom of Wakanda	Kingdom
2	Namor	Namor McKenzie	Marvel	Hero	$260,000,000,000	Entrepreneur	Atlantis	Kingdom
4	Iron Man	Tony Stark	Marvel	Hero	$100,000,000,000	Entrepreneur	Stark Industries	Multinational Conglomerate
5	Batman	Bruce Wayne	DC	Hero	$80,000,000,000	Inheritance	Wayne Enterprises	Multinational Conglomerate
11	Green Arrow	Oliver Queen	DC	Hero	$7,000,000,000	Inheritance	Queen Consolidated	Multinational Conglomerate
13	Iron Fist	Daniel Rand	Marvel	Hero	$5,000,000,000	Inheritance	Rand Enterprises	Multinational Conglomerate
14	Archangel	Warren Worthington III	Marvel	Hero	$5,000,000,000	Inheritance	Worthington Industries	Multinational Conglomerate
15	Blue Beetle	Ted Kord	DC	Hero	$5,000,000,000	Inheritance	Kord Enterprises	Multinational Conglomerate
17	Mister Fantastic	Reed Richards	Marvel	Hero	$5,000,000,000	Entrepreneur	Fantastic Four Inc	NaN
19	Crystal	Crystalia Amaquelin	Marvel	Hero	$4,000,000,000	Inheritance	NaN	NaN
20	Professor X	Charles Xavier	Marvel	Hero	$3,500,000,000	Inheritance	NaN	NaN
22	Black Bolt	Blackagar Boltagon	Marvel	Hero	$2,500,000,000	Self-made	Inhumans of Attilan	NaN
23	Moon Knight	Marc Spector	Marvel	Hero	$2,300,000,000	Investments	NaN	NaN
24	Silver Sable	Silvija Sablinova	Marvel	Hero	$2,100,000,000	Self-made	Silver Sable International	Mercenary Corporation
25	Spiderman	Peter Parker	Marvel	Hero	$2,000,000,000	Entrepreneur	Parker Industries	Tech Conglomerate
27	Nightwing	Dick Grayson	DC	Hero	$1,000,000,000	Inheritance	NaN	NaN
28	The Wasp	Janet van Dyne	Marvel	Hero	$1,000,000,000	Self-made	NaN	NaN
29	Mr. Terrific	Michael Holt	DC	Hero	$1,000,000,000	Entrepreneur	NaN	NaN
32	Michael Holt	Michael Holt	Marvel	Hero	$1,000,000,000	Entrepreneur	NaN	NaN
33	Star Sapphire	Carol Ferris	DC	Hero	$1,000,000,000	Inheritance	NaN	NaN
34	Power Girl	Kara Zor-L	DC	Hero	$1,000,000,000	Entrepreneur	NaN	NaN
In [4]:
# Show richest villain
villain_options = ["Type", "Villain"]
richest_villain = character_wealth_df[character_wealth_df["Type"].isin(villain_options)]
richest_villain
Out[4]:
	Name	Alter_ego	Franchise	Type	Net_worth	Income_source	Entity_name	Entity_type
3	Sunspot	Roberto da Costa	Marvel	Villain	$125,000,000,000	Inheritance	NaN	NaN
6	Lex Luthor	Alexander Luthor	DC	Villain	$75,000,000,000	Entrepreneur	LexCorp	Multinational Conglomerate
7	Doctor Doom	Victor von Doom	Marvel	Villain	$35,000,000,000	Monarch	Latveria	Kingdom
8	Kingpin	Wilson Fisk	Marvel	Villain	$30,000,000,000	Entrepreneur	NaN	NaN
9	Black Adam	Theo Ramses Djoser Teth-Adam	DC	Villain	$12,000,000,000	Monarch	Khandaq	Kingdom
10	Ozymandias	Adrian Veidt	DC	Villain	$7,000,000,000	Entrepreneur	Veidt Enterprises	Multinational Conglomerate
12	Green Goblin	Noram Osborn	Marvel	Villain	$5,000,000,000	Entrepreneur	Oscorp Industries	Multinational Conglomerate
16	Nighthawk	Kyle Richmond	Marvel	Villain	$5,000,000,000	Inheritance	Richmond Enterprises	Multinational Conglomerate
18	Simon Stagg	Simon Stagg	DC	Villain	$4,000,000,000	Entrepreneur	Stagg Industries	Multinational Conglomerate
21	White Queen	Emma Frost	Marvel	Villain	$3,000,000,000	Inheritance	Frost International	Export and Trading
26	Vandal Savage	Vandar Adg	DC	Villain	$2,000,000,000	Self-made	NaN	NaN
30	Maxwell Lord	Maxwell Lord	DC	Villain	$1,000,000,000	Entrepreneur	Black Gold Cooperative	Oil and Gas
31	Ra's Al Ghul	Ra's Al Ghul	DC	Villain	$1,000,000,000	Self-made	NaN	NaN
35	Medusa	Medusalith Amaquelin-Boltagon	Marvel	Villain	$1,000,000,000	Monarch	Inhumans of Attilan	NaN
36	Magneto	Erik Lehnsherr	Marvel	Villain	$900,000,000	Self-made	NaN	NaN
In [18]:
# Bar chart showing income source for number of characters
income_source_plot = character_wealth_df["Income_source"].value_counts()
income_source_plot.plot(kind = "bar", figsize = (8,6), color = ["forestgreen", "firebrick", "lightsalmon", "thistle","lightgray" ], edgecolor = "black")
plt.title ("Number of Income Source Types", fontweight = "bold", fontsize = 18)
plt.xlabel("Income Source", fontweight = "bold", fontsize = 14)
plt.ylabel("Number of Characters", fontweight = "bold", fontsize = 14)
plt.xticks(rotation = "0", fontsize = 12)
plt.grid()
 
In [38]:
# Pie chart
labels = ["Entrepreneur", "Inheritance", "Self-made", "Monarch", "Investments"]
sizes = [35.1, 32.2, 16.2, 13.5, 2.7]
colors = ["skyblue", "orange", "limegreen", "tomato", "thistle"]
explode = (0.05, 0.05, 0.05, 0.05, 0.05)
 
plt.pie(sizes, colors = colors, 
                        labels = labels,
                        autopct = "%1.1f%%", 
                        startangle = 90, 
                        pctdistance = 0.85, 
                        explode = explode)

centre_circle = plt.Circle((0,0),0.70, fc = "white")
fig = plt.gcf()
fig.gca().add_artist(centre_circle)
plt.tight_layout()
plt.title("Percentages of Each Income Source", fontweight = "bold", fontsize = 16)
plt.show()
 
%matplotlib notebook
In [208]:
import pandas as pd
import matplotlib.pyplot as plt
from matplotlib import lines
from matplotlib import patches
from matplotlib.patheffects import withStroke
import scipy.stats as st
import numpy as np
In [209]:
dc_data_df= pd.read_csv('../Project_1/dc-wikia-data_csv.csv')
In [210]:
marvel_data_df = pd.read_csv('../Project_1/marvel-wikia-data_csv.csv')
In [211]:
combined_hero_data = pd.merge(dc_data_df, marvel_data_df, how="outer")
In [212]:
#List all the heros
combined_hero_data
Out[212]:
	page_id	name	urlslug	id	align	eye	hair	sex	gsm	alive	appearances	first appearance	year
0	1422	batman (bruce wayne)	\/wiki\/batman_(bruce_wayne)	secret identity	good characters	blue eyes	black hair	male characters	straight	living characters	3093.0	1939, may	1939.0
1	23387	superman (clark kent)	\/wiki\/superman_(clark_kent)	secret identity	good characters	blue eyes	black hair	male characters	straight	living characters	2496.0	1986, october	1986.0
2	1458	green lantern (hal jordan)	\/wiki\/green_lantern_(hal_jordan)	secret identity	good characters	brown eyes	brown hair	male characters	straight	living characters	1565.0	1959, october	1959.0
3	1659	james gordon (new earth)	\/wiki\/james_gordon_(new_earth)	public identity	good characters	brown eyes	white hair	male characters	straight	living characters	1316.0	1987, february	1987.0
4	1576	richard grayson (new earth)	\/wiki\/richard_grayson_(new_earth)	secret identity	good characters	blue eyes	black hair	male characters	straight	living characters	1237.0	1940, april	1940.0
...	...	...	...	...	...	...	...	...	...	...	...	...	...
23267	657508	ru'ach (earth-616)	\/ru%27ach_(earth-616)	no dual identity	bad characters	green eyes	no hair	male characters	straight	living characters	NaN	NaN	NaN
23268	665474	thane (thanos' son) (earth-616)	\/thane_(thanos%27_son)_(earth-616)	no dual identity	good characters	blue eyes	bald	male characters	straight	living characters	NaN	NaN	NaN
23269	695217	tinkerer (skrull) (earth-616)	\/tinkerer_(skrull)_(earth-616)	secret identity	bad characters	black eyes	bald	male characters	straight	living characters	NaN	NaN	NaN
23270	708811	tk421 (spiderling) (earth-616)	\/tk421_(spiderling)_(earth-616)	secret identity	neutral characters	NaN	bald	male characters	straight	living characters	NaN	NaN	NaN
23271	673702	yologarch (earth-616)	\/yologarch_(earth-616)	NaN	bad characters	NaN	bald	NaN	straight	living characters	NaN	NaN	NaN
23272 rows × 13 columns
In [213]:
#How many characters in DC universe?
len(dc_data_df)
Out[213]:
6896
In [214]:
#How many characters in Marvel universe?
len(marvel_data_df)
Out[214]:
16376
In [215]:
#How many characters in each universe?
len(combined_hero_data)
Out[215]:
23272
In [216]:
dc_gender_df = pd.read_csv('../Project_1/dc-wikia-data_csv.csv')
dc_gender = dc_gender_df['sex']
In [217]:
#DC Universe genders
dc_gender
Out[217]:
0         male characters
1         male characters
2         male characters
3         male characters
4         male characters
              ...        
6891    female characters
6892      male characters
6893      male characters
6894      male characters
6895      male characters
Name: sex, Length: 6896, dtype: object
In [218]:
#Count the number of male, female, genderless, and transgender characters in DC Universe
dc_gender_count = dc_gender_df.groupby('sex')

dc_genders = dc_gender_count['sex'].count()

dc_genders
Out[218]:
sex
female characters         1967
genderless characters       20
male characters           4783
transgender characters       1
Name: sex, dtype: int64
In [219]:
#Bar Chart outlining genders in DC Universe
dc_gender_count = dc_gender_df['sex'].value_counts()


plt.xlabel("Genders")
plt.ylabel("Count of genders")

plt.title("Genders Count in the DC Universe")

bar_plot = dc_gender_count.plot.bar()
 
In [221]:
marvel_gender_df = pd.read_csv('../Project_1/marvel-wikia-data_csv.csv')
marvel_gender = marvel_gender_df['sex']
In [222]:
#Marvel Universe genders
marvel_gender
Out[222]:
0        male characters
1        male characters
2        male characters
3        male characters
4        male characters
              ...       
16371    male characters
16372    male characters
16373    male characters
16374    male characters
16375                NaN
Name: sex, Length: 16376, dtype: object
In [223]:
#Count the number of male, female, genderless, and transgender characters in Marvel Universe
marvel_gender_df['sex'].value_counts()
Out[223]:
male characters           11638
female characters          3837
agender characters           45
genderfluid characters        2
Name: sex, dtype: int64
In [231]:
marvel_gender_count = marvel_gender_df['sex'].value_counts()


plt.xlabel("Genders")
plt.ylabel("Count of genders")

plt.title("Genders Count in the Marvel Universe")

bar_plot = marvel_gender_count.plot.bar()
In [232]:
dc_eye_df = pd.read_csv('../Project_1/dc-wikia-data_csv.csv')
dc_eye = dc_eye_df['eye']
In [233]:
#Display breakdown of eye color in DC Universe
dc_eye_df['eye'].value_counts()
Out[233]:
blue eyes             1102
brown eyes             879
black eyes             412
green eyes             291
red eyes               208
white eyes             116
yellow eyes             86
photocellular eyes      48
grey eyes               40
hazel eyes              23
purple eyes             14
violet eyes             12
orange eyes             10
gold eyes                9
auburn hair              7
pink eyes                6
amber eyes               5
Name: eye, dtype: int64
In [234]:
labels = ["Blue Eyes", "Brown Eyes", "Black Eyes", "Green Eyes", "Red Eyes", "White Eyes", "Yellow Eyes", 
          "Photocellular Eyes", "Grey Eyes", "Hazel Eyes", "Purple Eyes", "Violet Eyes", "Orange Eyes", "Gold Eyes", 
          "Auburn Eyes","Pink Eyes","Amber Eyes"]

# The values of each section of the pie chart
sizes = [1102, 879, 412, 291, 208, 116, 86, 48, 40, 23, 14, 12, 10, 9, 7, 6, 5]

# The colors of each section of the pie chart
colors = ["Blue", "Brown", "Black", "Green", "Red", "White", "Yellow", 
          "White", "Grey", "lightcoral", "Purple", "Violet", "Orange", "Gold", 
          "lightskyblue","Pink","crimson"]

# Tells matplotlib to separate the "Eyes" section from the others
explode = (0.5, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0)
In [235]:
#Pie Chart showing breakdown of genders in Marvel Universe
dc_eye_pie = dc_eye_df["eye"].value_counts()
dc_eye_pie
dc_eye_pie.plot.pie(autopct = "%1.1f%%")
plt.title('Breakdown of Eye Color in DC Universe')
plt.show()
In [181]:
marvel_eye_df = pd.read_csv('../Project_1/marvel-wikia-data_csv.csv')
marvel_eye = marvel_eye_df['eye']
In [182]:
#Display breakdown of eye color in Marvel Universe
marvel_eye_df['eye'].value_counts()
Out[182]:
blue eyes          1962
brown eyes         1924
green eyes          613
black eyes          555
red eyes            508
white eyes          400
yellow eyes         256
grey eyes            95
hazel eyes           76
variable eyes        49
purple eyes          31
orange eyes          25
pink eyes            21
one eye              21
gold eyes            14
silver eyes          12
violet eyes          11
amber eyes           10
multiple eyes         7
no eyes               7
yellow eyeballs       6
black eyeballs        3
magenta eyes          2
compound eyes         1
Name: eye, dtype: int64
In [192]:
eyes = ["Blue Eyes", "Brown Eyes", "Green Eyes", "Black Eyes", "Red Eyes", "White Eyes", "Yellow Eyes", 
          "Grey Eyes", "Hazel Eyes", "Variable Eyes", "Purple Eyes", "Orange Eyes", "Pink Eyes", 
          "One Eye","Gold Eyes","Silver Eyes", "Violet Eye","Amber Eyes","Multiple Eyes",  
        "No Eyes","Yellow Eyesballs","Black Eyesballs", "Magenta Eye","Compound Eyes"]

# The values of each section of the pie chart
sizes = [1962, 1924, 613, 555, 508, 400, 256, 95, 76, 49, 31, 25, 21, 21, 14, 12, 11, 10, 7, 7, 6, 3, 2, 1]

# The colors of each section of the pie chart
colors = ["Blue", "Brown", "Green", "Black", "Red", "White", "Yellow", 
          "Grey", "lightcoral", "yellowgreen", "Purple", "Orange", "Pink", 
          "beige","Gold","Silver", "Violet","crimson","lightblue",  
        "lightgreen","lightyellow","darkgreen", "Magenta","lightgrey"]

# Tells matplotlib to separate the "Eyes" section from the others
explode = (0.5, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0)
In [236]:
marvel_eye_pie = marvel_eye_df["eye"].value_counts()
marvel_eye_pie
marvel_eye_pie.plot.pie(autopct = "%1.1f%%")
plt.title('Breakdown of Eye Color in Marvel Universe')
plt.show()
In [237]:
dc_orientation_df = pd.read_csv('../Project_1/dc-wikia-data_csv.csv')
dc_orientation = dc_orientation_df['gsm']
In [238]:
#Display breakdown of sexual orientation in DC Universe
dc_orientation_df['gsm'].value_counts()
Out[238]:
straight                 6832
homosexual characters      54
bisexual characters        10
Name: gsm, dtype: int64
In [239]:
dc_orientation = dc_orientation_df["gsm"].value_counts()
dc_orientation.plot.pie(autopct= "%1.1f%%")
plt.title("Breakdown of sexual orientation in DC Universe")
plt.show()
In [240]:
marvel_orientation_df = pd.read_csv('../Project_1/marvel-wikia-data_csv.csv')
marvel_orientation = marvel_orientation_df['gsm']
In [241]:
#Breakdown of sexual orientation in Marvel Universe
marvel_orientation_df['gsm'].value_counts()
Out[241]:
straight                  16286
homosexual characters        66
bisexual characters          19
transgender characters        2
transvestites                 1
pansexual characters          1
genderfluid characters        1
Name: gsm, dtype: int64
In [242]:
#Pie Chart showing breakdown of sexual orientations in Marvel Universe
marvel_orientation = marvel_orientation_df["gsm"].value_counts()
marvel_orientation.plot.pie(autopct= "%1.1f%%")
plt.title("Breakdown of sexual orientation in Marvel Universe")
plt.show()
In [243]:
dc_appearances_df = pd.read_csv('../Project_1/dc-wikia-data_csv.csv')
dc_appearances = dc_appearances_df['appearances']
In [244]:
#Who has made the most appearances in the DC Universe?
dc_appearances_df = dc_appearances_df[['name', 'appearances']]

dc_appearances_df.head()
Out[244]:
	name	appearances
0	batman (bruce wayne)	3093.0
1	superman (clark kent)	2496.0
2	green lantern (hal jordan)	1565.0
3	james gordon (new earth)	1316.0
4	richard grayson (new earth)	1237.0
In [245]:
marvel_appearances_df = pd.read_csv('../Project_1/marvel-wikia-data_csv.csv')
marvel_appearances = marvel_appearances_df['appearances']
In [246]:
#Who has made the most appearances in the Marvel Universe?
marvel_appearances_df = marvel_appearances_df[['name', 'appearances']]

marvel_appearances_df.head()
Out[246]:
	name	appearances
0	spider-man (peter parker)	4043.0
1	captain america (steven rogers)	3360.0
2	wolverine (james \"logan\" howlett)	3061.0
3	iron man (anthony \"tony\" stark)	2961.0
4	thor (thor odinson)	2258.0
