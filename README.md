# Full-Stack-Assignmnt
Bash :
npx create-react-app movie-app
cd movie-app
npm install axios react-router-dom
JSX :
// App.js
import React from 'react';
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
import MovieSearch from './components/MovieSearch';
import MovieDetails from './components/MovieDetails';
import SimilarMovies from './components/SimilarMovies';
import UserAuth from './components/UserAuth';
import Favorites from './components/Favorites';

function App() {
  return (
    <Router>
      <Switch>
        <Route path="/" exact component={MovieSearch} />
        <Route path="/movie/:id" component={MovieDetails} />
        <Route path="/similar/:id" component={SimilarMovies} />
        <Route path="/login" component={UserAuth} />
        <Route path="/favorites" component={Favorites} />
      </Switch>
    </Router>
  );
}
export default MovieSearch;
CSS :
/* Styling for the MovieSearch component */
.movie-search {
  padding: 20px;
}

.movie-search h1 {
  font-size: 24px;
  margin-bottom: 10px;
}

.movie-search form {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}

.movie-search input {
  flex: 1;
  padding: 8px;
  font-size: 16px;
}

.movie-search button {
  margin-left: 10px;
  padding: 8px 16px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.movie-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}

.movie-item {
  border: 1px solid #ccc;
  padding: 10px;
  border-radius: 4px;
}

.movie-item h2 {
  font-size: 20px;
  margin-bottom: 8px;
}

.movie-item p {
  margin-bottom: 5px;
}
PHP :
// routes/api.php
Route::group(['prefix' => 'movies'], function () {
    Route::get('/search', 'App\Http\Controllers\MovieController@search');
    Route::get('/{id}', 'App\Http\Controllers\MovieController@getMovieDetails');
    Route::get('/similar/{id}', 'App\Http\Controllers\MovieController@getSimilarMovies');
});

Route::group(['prefix' => 'favorites'], function () {
    Route::post('/add', 'App\Http\Controllers\UserController@addToFavorites');
    Route::get('/{user_id}', 'App\Http\Controllers\UserController@getFavorites');
    Route::delete('/remove/{user_id}/{movie_id}', 'App\Http\Controllers\UserController@removeFromFavorites');
});

Route::group(['prefix' => 'auth'], function () {
    Route::post('/signup', 'App\Http\Controllers\UserController@signup');
    Route::post('/login', 'App\Http\Controllers\UserController@login');
});
bash :
php artisan migrate
JSX with bootstrap :
import React, { useState } from 'react';
import axios from 'axios';

const MovieSearch = () => {
  const [query, setQuery] = useState('');
  const [movies, setMovies] = useState([]);

  const handleSearch = async (e) => {
    e.preventDefault();
    try {
      const response = await axios.get(
        `YOUR_BACKEND_API_URL/movies/search?query=${query}`
      );
      setMovies(response.data.results);
    } catch (error) {
      console.error('Error fetching movies:', error);
    }
  };

  return (
    <div className="container mt-4">
      <h1 className="mb-4">Movie Search</h1>
      <form onSubmit={handleSearch} className="mb-4">
        <div className="input-group">
          <input
            type="text"
            className="form-control"
            placeholder="Search for a movie..."
            value={query}
            onChange={(e) => setQuery(e.target.value)}
          />
          <button type="submit" className="btn btn-primary">Search</button>
        </div>
      </form>
      <div className="row">
        {movies.map((movie) => (
          <div className="col-md-4" key={movie.id}>
            <div className="card mb-4 shadow">
              <div className="card-body">
                <h5 className="card-title">{movie.title}</h5>
                <p className="card-text">Release Date: {movie.release_date}</p>
                <p className="card-text">{movie.overview}</p>
                <p className="card-text">Rating: {movie.vote_average}</p>
                {/* Add a link to view more details about the movie */}
              </div>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
};

export default MovieSearch;

