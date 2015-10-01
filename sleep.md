#!/bin/bash

echo "paper rock scissors"
echo "What do you choose?"
read rps #rps=rock, paper, scissors

case $rps in
rock) sleep 2s; echo "Tie:  Rock, vs. Rock" ;;
paper) sleep 2s; echo "You win:  Paper beats rock!" ;;
scissors) sleep 2s; echo "Computer wins:  Rock beats scissors!";;
esac
