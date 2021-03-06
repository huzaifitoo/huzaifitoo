- š Hi, Iām @huzaifitoo
- š Iām interested in ...
- š± Iām currently learning ...
- šļø Iām looking to collaborate on ...
- š« How to reach me ...

<!---
huzaifitoo/huzaifitoo is a āØ special āØ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
"cells": [
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [],
   "source": [
    "import pandas as pd\n",
    "import numpy as np"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {},
   "outputs": [],
   "source": [
    "from rake_nltk import Rake\n",
    "import numpy as np"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.metrics.pairwise import cosine_similarity\n",
    "from sklearn.feature_extraction.text import CountVectorizer"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Index(['index', 'director', 'num_critic_for_reviews', 'duration',\n",
       "       'director_facebook_likes', 'actor_3_facebook_likes', 'actor1',\n",
       "       'actor_1_facebook_likes', 'gross', 'genres', 'actor2', 'Title',\n",
       "       'num_voted_users', 'cast_total_facebook_likes', 'actor3',\n",
       "       'facenumber_in_poster', 'plot_keywords', 'movie_imdb_link',\n",
       "       'num_user_for_reviews', 'language', 'country', 'content_rating',\n",
       "       'budget', 'title_year', 'actor_2_facebook_likes', 'imdb_score',\n",
       "       'aspect_ratio', 'movie_facebook_likes'],\n",
       "      dtype='object')"
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df=pd.read_csv(\"movie_metadata.csv\")\n",
    "df.columns"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>index</th>\n",
       "      <th>director</th>\n",
       "      <th>num_critic_for_reviews</th>\n",
       "      <th>duration</th>\n",
       "      <th>director_facebook_likes</th>\n",
       "      <th>actor_3_facebook_likes</th>\n",
       "      <th>actor1</th>\n",
       "      <th>actor_1_facebook_likes</th>\n",
       "      <th>gross</th>\n",
       "      <th>genres</th>\n",
       "      <th>...</th>\n",
       "      <th>num_user_for_reviews</th>\n",
       "      <th>language</th>\n",
       "      <th>country</th>\n",
       "      <th>content_rating</th>\n",
       "      <th>budget</th>\n",
       "      <th>title_year</th>\n",
       "      <th>actor_2_facebook_likes</th>\n",
       "      <th>imdb_score</th>\n",
       "      <th>aspect_ratio</th>\n",
       "      <th>movie_facebook_likes</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>0</td>\n",
       "      <td>James Cameron</td>\n",
       "      <td>723.0</td>\n",
       "      <td>178.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>855.0</td>\n",
       "      <td>Joel David Moore</td>\n",
       "      <td>1000.0</td>\n",
       "      <td>760505847.0</td>\n",
       "      <td>Action|Adventure|Fantasy|Sci-Fi</td>\n",
       "      <td>...</td>\n",
       "      <td>3054.0</td>\n",
       "      <td>English</td>\n",
       "      <td>USA</td>\n",
       "      <td>PG-13</td>\n",
       "      <td>237000000.0</td>\n",
       "      <td>2009.0</td>\n",
       "      <td>936.0</td>\n",
       "      <td>7.9</td>\n",
       "      <td>1.78</td>\n",
       "      <td>33000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>1</td>\n",
       "      <td>Gore Verbinski</td>\n",
       "      <td>302.0</td>\n",
       "      <td>169.0</td>\n",
       "      <td>563.0</td>\n",
       "      <td>1000.0</td>\n",
       "      <td>Orlando Bloom</td>\n",
       "      <td>40000.0</td>\n",
       "      <td>309404152.0</td>\n",
       "      <td>Action|Adventure|Fantasy</td>\n",
       "      <td>...</td>\n",
       "      <td>1238.0</td>\n",
       "      <td>English</td>\n",
       "      <td>USA</td>\n",
       "      <td>PG-13</td>\n",
       "      <td>300000000.0</td>\n",
       "      <td>2007.0</td>\n",
       "      <td>5000.0</td>\n",
       "      <td>7.1</td>\n",
       "      <td>2.35</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>2</td>\n",
       "      <td>Sam Mendes</td>\n",
       "      <td>602.0</td>\n",
       "      <td>148.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>161.0</td>\n",
       "      <td>Rory Kinnear</td>\n",
       "      <td>11000.0</td>\n",
       "      <td>200074175.0</td>\n",
       "      <td>Action|Adventure|Thriller</td>\n",
       "      <td>...</td>\n",
       "      <td>994.0</td>\n",
       "      <td>English</td>\n",
       "      <td>UK</td>\n",
       "      <td>PG-13</td>\n",
       "      <td>245000000.0</td>\n",
       "      <td>2015.0</td>\n",
       "      <td>393.0</td>\n",
       "      <td>6.8</td>\n",
       "      <td>2.35</td>\n",
       "      <td>85000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>3</td>\n",
       "      <td>Christopher Nolan</td>\n",
       "      <td>813.0</td>\n",
       "      <td>164.0</td>\n",
       "      <td>22000.0</td>\n",
       "      <td>23000.0</td>\n",
       "      <td>Christian Bale</td>\n",
       "      <td>27000.0</td>\n",
       "      <td>448130642.0</td>\n",
       "      <td>Action|Thriller</td>\n",
       "      <td>...</td>\n",
       "      <td>2701.0</td>\n",
       "      <td>English</td>\n",
       "      <td>USA</td>\n",
       "      <td>PG-13</td>\n",
       "      <td>250000000.0</td>\n",
       "      <td>2012.0</td>\n",
       "      <td>23000.0</td>\n",
       "      <td>8.5</td>\n",
       "      <td>2.35</td>\n",
       "      <td>164000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>4</td>\n",
       "      <td>Doug Walker</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>131.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>Rob Walker</td>\n",
       "      <td>131.0</td>\n",
       "      <td>NaN</td>\n",
       "      <td>Documentary</td>\n",
       "      <td>...</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>12.0</td>\n",
       "      <td>7.1</td>\n",
       "      <td>NaN</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>5 rows Ć 28 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "   index           director  num_critic_for_reviews  duration  \\\n",
       "0      0      James Cameron                   723.0     178.0   \n",
       "1      1     Gore Verbinski                   302.0     169.0   \n",
       "2      2         Sam Mendes                   602.0     148.0   \n",
       "3      3  Christopher Nolan                   813.0     164.0   \n",
       "4      4        Doug Walker                     NaN       NaN   \n",
       "\n",
       "   director_facebook_likes  actor_3_facebook_likes            actor1  \\\n",
       "0                      0.0                   855.0  Joel David Moore   \n",
       "1                    563.0                  1000.0     Orlando Bloom   \n",
       "2                      0.0                   161.0      Rory Kinnear   \n",
       "3                  22000.0                 23000.0    Christian Bale   \n",
       "4                    131.0                     NaN        Rob Walker   \n",
       "\n",
       "   actor_1_facebook_likes        gross                           genres  \\\n",
       "0                  1000.0  760505847.0  Action|Adventure|Fantasy|Sci-Fi   \n",
       "1                 40000.0  309404152.0         Action|Adventure|Fantasy   \n",
       "2                 11000.0  200074175.0        Action|Adventure|Thriller   \n",
       "3                 27000.0  448130642.0                  Action|Thriller   \n",
       "4                   131.0          NaN                      Documentary   \n",
       "\n",
       "          ...          num_user_for_reviews language  country  content_rating  \\\n",
       "0         ...                        3054.0  English      USA           PG-13   \n",
       "1         ...                        1238.0  English      USA           PG-13   \n",
       "2         ...                         994.0  English       UK           PG-13   \n",
       "3         ...                        2701.0  English      USA           PG-13   \n",
       "4         ...                           NaN      NaN      NaN             NaN   \n",
       "\n",
       "        budget  title_year actor_2_facebook_likes imdb_score  aspect_ratio  \\\n",
       "0  237000000.0      2009.0                  936.0        7.9          1.78   \n",
       "1  300000000.0      2007.0                 5000.0        7.1          2.35   \n",
       "2  245000000.0      2015.0                  393.0        6.8          2.35   \n",
       "3  250000000.0      2012.0                23000.0        8.5          2.35   \n",
       "4          NaN         NaN                   12.0        7.1           NaN   \n",
       "\n",
       "  movie_facebook_likes  \n",
       "0                33000  \n",
       "1                    0  \n",
       "2                85000  \n",
       "3               164000  \n",
       "4                    0  \n",
       "\n",
       "[5 rows x 28 columns]"
      ]
     },
     "execution_count": 5,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(5043, 28)"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {},
   "outputs": [],
   "source": [
    "def get_title_from_index(index):\n",
    "    return  df[df.index==index][\"Title\"].values[0]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {},
   "outputs": [],
   "source": [
    "def get_index_from_title(Title):\n",
    "    return df[df.Title==Title][\"index\"].values[0]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {},
   "outputs": [],
   "source": [
    "features=[\"Title\",\"genres\",\"director\",\"actor1\",\"actor2\",\"actor3\"]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "['Title', 'genres', 'director', 'actor1', 'actor2', 'actor3']\n"
     ]
    }
   ],
   "source": [
    "print(features)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "metadata": {},
   "outputs": [],
   "source": [
    "def combine_features(row):\n",
    "    return row[\"Title\"]+\"\"+row[\"genres\"]+\"\"+row[\"director\"]+\"\"+row[\"actor1\"]+\"\"+row[\"actor2\"]+\"\"+row[\"actor3\"]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "metadata": {},
   "outputs": [],
   "source": [
    "for feature in features:\n",
    "    df[feature]=df[feature].fillna(\"\")\n",
    "df[\"combined_features\"]=df.apply(combine_features,axis=1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "0       Avatar Action|Adventure|Fantasy|Sci-FiJames Ca...\n",
      "1       Pirates of the Caribbean: At World's End Actio...\n",
      "2       Spectre Action|Adventure|ThrillerSam MendesRor...\n",
      "3       The Dark Knight Rises Action|ThrillerChristoph...\n",
      "4       Star Wars: Episode VII - The Force Awakens    ...\n",
      "5       John Carter Action|Adventure|Sci-FiAndrew Stan...\n",
      "6       Spider-Man 3 Action|Adventure|RomanceSam Raimi...\n",
      "7       Tangled Adventure|Animation|Comedy|Family|Fant...\n",
      "8       Avengers: Age of Ultron Action|Adventure|Sci-F...\n",
      "9       Harry Potter and the Half-Blood Prince Adventu...\n",
      "10      Batman v Superman: Dawn of Justice Action|Adve...\n",
      "11      Superman Returns Action|Adventure|Sci-FiBryan ...\n",
      "12      Quantum of Solace Action|AdventureMarc Forster...\n",
      "13      Pirates of the Caribbean: Dead Man's Chest Act...\n",
      "14      The Lone Ranger Action|Adventure|WesternGore V...\n",
      "15      Man of Steel Action|Adventure|Fantasy|Sci-FiZa...\n",
      "16      The Chronicles of Narnia: Prince Caspian Actio...\n",
      "17      The Avengers Action|Adventure|Sci-FiJoss Whedo...\n",
      "18      Pirates of the Caribbean: On Stranger Tides Ac...\n",
      "19      Men in Black 3 Action|Adventure|Comedy|Family|...\n",
      "20      The Hobbit: The Battle of the Five Armies Adve...\n",
      "21      The Amazing Spider-Man Action|Adventure|Fantas...\n",
      "22      Robin Hood Action|Adventure|Drama|HistoryRidle...\n",
      "23      The Hobbit: The Desolation of Smaug Adventure|...\n",
      "24      The Golden Compass Adventure|Family|FantasyChr...\n",
      "25      King Kong Action|Adventure|Drama|RomancePeter ...\n",
      "26      Titanic Drama|RomanceJames CameronKate Winslet...\n",
      "27      Captain America: Civil War Action|Adventure|Sc...\n",
      "28      Battleship Action|Adventure|Sci-Fi|ThrillerPet...\n",
      "29      Jurassic World Action|Adventure|Sci-Fi|Thrille...\n",
      "                              ...                        \n",
      "5013    Manito Drama|FamilyEric EasonPanchito GĆ³mezFra...\n",
      "5014    Rampage Action|Crime|ThrillerUwe BollKatharine...\n",
      "5015    Slacker Comedy|DramaRichard LinklaterRichard L...\n",
      "5016    Dutch Kills Crime|Drama|ThrillerJoseph Mazzell...\n",
      "5017    Dry Spell Comedy|RomanceTravis LeggeSuzi Lorra...\n",
      "5018    Flywheel DramaAlex KendrickLisa ArnoldShannen ...\n",
      "5019    Exeter Horror|Mystery|ThrillerMarcus NispelBri...\n",
      "5020    The Ridges Drama|Horror|ThrillerBrandon Lander...\n",
      "5021    The Puffy Chair Comedy|Drama|RomanceJay Duplas...\n",
      "5022    Stories of Our Lives DramaJim ChuchuOlwenya Ma...\n",
      "5023    Breaking Upwards RomanceDaryl WeinHeather Burn...\n",
      "5024    All Superheroes Must Die Sci-Fi|ThrillerJason ...\n",
      "5025    Pink Flamingos Comedy|Crime|HorrorJohn WatersM...\n",
      "5026    Clean Drama|Music|RomanceOlivier AssayasBĆ©atri...\n",
      "5027    The Circle DramaJafar PanahiNargess MamizadehF...\n",
      "5028    Tin Can Man HorrorIvan KavanaghMichael ParlePa...\n",
      "5029    The Cure Crime|Horror|Mystery|ThrillerKiyoshi ...\n",
      "5030    On the Downlow DramaTadeo GarciaMichael Cortez...\n",
      "5031    Sanctuary; Quite a Conundrum Comedy|Horror|Thr...\n",
      "5032    Bang Crime|DramaAsh Baron-CohenStanley B. Herm...\n",
      "5033    Primer Drama|Sci-Fi|ThrillerShane CarruthDavid...\n",
      "5034    Cavite ThrillerNeill Dela LlanaEdgar Tancangco...\n",
      "5035    El Mariachi Action|Crime|Drama|Romance|Thrille...\n",
      "5036    The Mongol King Crime|DramaAnthony ValloneJohn...\n",
      "5037    Newlyweds Comedy|DramaEdward BurnsCaitlin Fitz...\n",
      "5038    Signed Sealed Delivered Comedy|DramaScott Smit...\n",
      "5039    The Following             Crime|Drama|Mystery|...\n",
      "5040    A Plague So Pleasant Drama|Horror|ThrillerBenj...\n",
      "5041    Shanghai Calling Comedy|Drama|RomanceDaniel Hs...\n",
      "5042    My Date with Drew DocumentaryJon GunnBrian Her...\n",
      "Name: combined_features, Length: 5043, dtype: object\n"
     ]
    }
   ],
   "source": [
    "print(df[\"combined_features\"])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "metadata": {},
   "outputs": [],
   "source": [
    "df[\"combined_features\"]=df[\"combined_features\"].str.replace(\"|\",\" \")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0    Avatar Action Adventure Fantasy Sci-FiJames Ca...\n",
       "1    Pirates of the Caribbean: At World's End Actio...\n",
       "2    Spectre Action Adventure ThrillerSam MendesRor...\n",
       "3    The Dark Knight Rises Action ThrillerChristoph...\n",
       "4    Star Wars: Episode VII - The Force Awakens    ...\n",
       "Name: combined_features, dtype: object"
      ]
     },
     "execution_count": 15,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df[\"combined_features\"].head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "  (0, 20711)\t1\n",
      "  (0, 16911)\t1\n",
      "  (0, 14640)\t1\n",
      "  (0, 4919)\t1\n",
      "  (0, 2891)\t1\n",
      "  (0, 7417)\t1\n",
      "  (0, 18980)\t1\n",
      "  (0, 6945)\t1\n",
      "  (0, 220)\t1\n",
      "  (0, 157)\t1\n",
      "  (0, 992)\t1\n",
      "  (1, 4911)\t1\n",
      "  (1, 5179)\t1\n",
      "  (1, 1934)\t1\n",
      "  (1, 22353)\t1\n",
      "  (1, 6993)\t1\n",
      "  (1, 6574)\t1\n",
      "  (1, 23740)\t1\n",
      "  (1, 927)\t1\n",
      "  (1, 3027)\t1\n",
      "  (1, 21120)\t1\n",
      "  (1, 15766)\t1\n",
      "  (1, 16614)\t1\n",
      "  (1, 220)\t1\n",
      "  (1, 157)\t1\n",
      "  :\t:\n",
      "  (5040, 21290)\t1\n",
      "  (5040, 16714)\t1\n",
      "  (5040, 16677)\t1\n",
      "  (5040, 19891)\t1\n",
      "  (5040, 3295)\t1\n",
      "  (5040, 10346)\t1\n",
      "  (5040, 5718)\t1\n",
      "  (5041, 4318)\t1\n",
      "  (5041, 18511)\t1\n",
      "  (5041, 9859)\t1\n",
      "  (5041, 10548)\t1\n",
      "  (5041, 2873)\t1\n",
      "  (5041, 18092)\t1\n",
      "  (5041, 19286)\t1\n",
      "  (5041, 5718)\t1\n",
      "  (5041, 3850)\t1\n",
      "  (5042, 9217)\t1\n",
      "  (5042, 974)\t1\n",
      "  (5042, 9933)\t1\n",
      "  (5042, 9218)\t1\n",
      "  (5042, 5508)\t1\n",
      "  (5042, 6071)\t1\n",
      "  (5042, 15133)\t1\n",
      "  (5042, 4904)\t1\n",
      "  (5042, 23602)\t1\n"
     ]
    }
   ],
   "source": [
    "c=CountVectorizer()\n",
    "count_matrix=c.fit_transform(df[\"combined_features\"])\n",
    "print(count_matrix)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "[[1.         0.16116459 0.21320072 ... 0.         0.         0.        ]\n",
      " [0.16116459 1.         0.18898224 ... 0.         0.         0.        ]\n",
      " [0.21320072 0.18898224 1.         ... 0.         0.         0.        ]\n",
      " ...\n",
      " [0.         0.         0.         ... 1.         0.10540926 0.        ]\n",
      " [0.         0.         0.         ... 0.10540926 1.         0.        ]\n",
      " [0.         0.         0.         ... 0.         0.         1.        ]]\n"
     ]
    }
   ],
   "source": [
    "cosine_sim=cosine_similarity(count_matrix)\n",
    "print(cosine_sim)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(5043, 5043)"
      ]
     },
     "execution_count": 18,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "cosine_sim.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "metadata": {},
   "outputs": [],
   "source": [
    "def recommended(movie_user_likes):\n",
    "    movie_index=get_index_from_title(movie_user_likes)\n",
    "    similar_movies=list(enumerate(cosine_sim[movie_index]))\n",
    "    sorted_similar_movies=sorted(similar_movies,key=lambda x:x[1],reverse=True)\n",
    "    i=0\n",
    "    for movie in sorted_similar_movies:\n",
    "      print(get_title_from_index(movie[0]))\n",
    "      i=i+1\n",
    "      if i>10:\n",
    "         break"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Click \n",
      "Practical Magic \n",
      "Shallow Hal \n",
      "Ghost Town \n",
      "The Tempest \n",
      "Big \n",
      "Sliding Doors \n",
      "Trollhunter \n",
      "The Family Man \n",
      "17 Again \n",
      "Stranger Than Fiction \n"
     ]
    }
   ],
   "source": [
    "recommended(\"Click\\xa0\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.7.1"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}
