// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC721/extensions/ERC721URIStorage.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

/**
 * @title CosmicJuanNFT
 * @dev Contrato inteligente para el ecosistema Cosmicjuan.blockchain
 * Implementa estándares de seguridad y lógica constructiva.
 */
contract CosmicJuanNFT is ERC721URIStorage, Ownable {
    uint256 private _nextTokenId;

    constructor() ERC721("CosmicJuan", "CJ") Ownable(msg.sender) {}

    /**
     * @dev Función para crear un nuevo NFT (Minting)
     * @param a Dirección que recibirá el token
     * @param uri Enlace a los metadatos (JSON/Imagen)
     */
    function safeMint(address a, string memory uri) public onlyOwner {
        uint256 tokenId = _nextTokenId++;
        _safeMint(a, tokenId);
        _setTokenURI(tokenId, uri);
    }

    // Las siguientes funciones son obligatorias por Solidity para manejar la herencia correctamente
    function supportsInterface(bytes4 interfaceId)
        public
        view
        override(ERC721URIStorage)
        returns (bool)
    {
        return super.supportsInterface(interfaceId);
    }

    function tokenURI(uint256 tokenId)
        public
        view
        override(ERC721URIStorage)
        returns (string memory)
    {
        return super.tokenURI(tokenId);
    }
}
