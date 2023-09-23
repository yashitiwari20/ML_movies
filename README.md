# ML_movies

import streamlit as st
import pickle
import numpy as np
import pandas as pd

def recommend(movie):
    movie_index = np.where(movies_list == movie)[0][0]  # Find the index in the NumPy array
    distances = similarity[movie_index]
    movies_list_with_titles = pd.DataFrame({'title': movies_list})  # Create a DataFrame with movie titles
    movies_list_with_titles['similarity'] = distances
    sorted_movies = movies_list_with_titles.sort_values(by='similarity', ascending=False)
    recommend_movies = sorted_movies['title'].tolist()[1:6]  # Exclude the selected movie itself

    movie_id=i[0]
    #fetch poster
    
    return recommend_movies

# Load movie data
movies_list = pickle.load(open('movies.pkl', 'rb'))
movies_list = movies_list['title'].values
similarity = pickle.load(open('similarity.pkl', 'rb'))

st.title('Movies Recommender System')

selected_movie_name = st.selectbox('Which type of movie do you want?', movies_list)

if st.button('Recommend'):
    recommendations = recommend(selected_movie_name)
    for i in recommendations:
        st.write(i)
