import React from "react";

const mockMatches = [ { player1: "Novak Djokovic", player2: "Wildcard Player", odds1: 1.01, odds2: 17.0, }, { player1: "Carlos Alcaraz", player2: "Qualifier X", odds1: 1.05, odds2: 11.0, }, { player1: "Iga Swiatek", player2: "Lucky Loser", odds1: 1.02, odds2: 20.0, }, ];

function getImpliedProbability(decimalOdds) { return +(1 / decimalOdds).toFixed(4); }

export default function TennisOddsDashboard() { const highConfidenceMatches = mockMatches.filter((match) => { const prob1 = getImpliedProbability(match.odds1); const prob2 = getImpliedProbability(match.odds2); return prob1 >= 0.99 || prob2 >= 0.99; });

return ( <div className="p-6 bg-gray-100 min-h-screen"> <h1 className="text-3xl font-bold mb-4">99% Predictable Tennis Matches</h1> <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4"> {highConfidenceMatches.map((match, index) => { const prob1 = getImpliedProbability(match.odds1); const prob2 = getImpliedProbability(match.odds2); const favorite = prob1 > prob2 ? match.player1 : match.player2; const prob = Math.max(prob1, prob2);

return (
        <div
          key={index}
          className="bg-white p-4 rounded-2xl shadow-md border-l-4 border-green-500"
        >
          <h2 className="text-xl font-semibold mb-2">
            {match.player1} vs {match.player2}
          </h2>
          <p>
            <strong>Favorite:</strong> {favorite}
          </p>
          <p>
            <strong>Win Probability:</strong> {(prob * 100).toFixed(2)}%
          </p>
        </div>
      );
    })}
  </div>
</div>

); }

