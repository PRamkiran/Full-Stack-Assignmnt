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

export default App;
