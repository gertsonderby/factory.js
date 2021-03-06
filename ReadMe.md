# Factory.js

A library for create test-data factories

## Usage

    function Game(data) {
        this.id = data.id;
        this.isOver = data.isOver;
        this.createAt = data.createAt;
        this.randomSeed = data.randomSeed;
        this.players = data.players;
    }

    function Player(data) {
        this.id = data.id;
        this.name = data.name;
    }

    var playerFactory = factory(function (name) {
        var id = this.sequence();
        name = name || 'Player ' + id;
        return new Player({
            id: id,
            name: name
        });
    });

    var gameFactory = factory(function () {
        var players = playerFactory.create(2);
        players.push(playerFactory('Awesome player'));
        return new Game({
            id: this.sequence(),
            isOver: false,
            createAt: new Date(),
            randomSeed: Math.random(),
            players: players
        });
    });

You can now build a new game the following way:

    var game = gameFactory();

which returns a Game instance with the following data:

    id: 0,
    isOver: true,
    createdAt: Wed Apr 03 2013 21:56:16 GMT+0200 (CEST),
    randomSeed: 0.672447538934648,
    players: [
        { id: 0, name: 'Player 0' },
        { id: 1, name: 'Player 1' },
        { id: 2, name: 'Awesome player' }
    ]

## License

    Copyright 2012 Sune Simonsen

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
