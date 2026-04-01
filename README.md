# On-chain-game-rock-paper-scissors-commit-reveal-
On‑chain game: rock‑paper‑scissors (commit‑reveal)
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract RPS {
    enum Move { None, Rock, Paper, Scissors }

    struct Player {
        bytes32 commit;
        Move move;
    }

    Player public p1;
    Player public p2;

    function commitP1(bytes32 c) public { p1.commit = c; }
    function commitP2(bytes32 c) public { p2.commit = c; }

    function revealP1(Move m, bytes32 salt) public {
        require(keccak256(abi.encodePacked(m, salt)) == p1.commit, "Invalid");
        p1.move = m;
    }

    function revealP2(Move m, bytes32 salt) public {
        require(keccak256(abi.encodePacked(m, salt)) == p2.commit, "Invalid");
        p2.move = m;
    }
}
