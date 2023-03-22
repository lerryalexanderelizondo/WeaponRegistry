// Declaration of the MIT license

// This contract registers the serial number of each weapon tested by the Proof House of the Worshipful Company of Gunmakers and issues a sales permit

// based on the test results

// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;

contract WeaponRegistry {

    // Data structure to store information about the weapons

    struct Weapon {

        uint serialNumber;

        bool approved;

    }

    // Mapping to associate a weapon with its serial number

    mapping (uint => Weapon) public weapons;

    // Event to notify when a new weapon has been registered

    event WeaponRegistered(uint serialNumber, bool approved);

    // Function to register a new weapon on the blockchain

    function registerWeapon(uint _serialNumber, bool _approved) public {

        // Check that the serial number is not already registered

        require(weapons[_serialNumber].serialNumber != _serialNumber, "This serial number has already been registered");

        // Create a new weapon in the mapping

        weapons[_serialNumber] = Weapon(_serialNumber, _approved);

        // Emit the registration event

        emit WeaponRegistered(_serialNumber, _approved);

    }

    // Function to verify if a weapon has a sales permit

    function verifySalesPermit(uint _serialNumber) public view returns (bool) {

        // Check if the weapon is approved

        if (weapons[_serialNumber].approved == true) {

            return true;

        } else {

            return false;

        }

    }

}

 
