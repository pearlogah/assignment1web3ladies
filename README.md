# assignment1web3ladies
// SPDX-License-Identifier:MIT:
pragma solidity ^0.8.0;

contract HealthRecordRepository {
    address public owner;
    
    struct Patient {
        string name;
        uint256 age;
        string gender;
        uint256 weight;
        uint256 height;
        string diagnosis;
        bool isAdmitted;
    }

    mapping(address => Patient) public patients;

    constructor() {
        owner = msg.sender;
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Only the owner can access this function.");
        _;
    }

    function addPatientRecord(
        string memory _name,
        uint256 _age,
        string memory _gender,
        uint256 _weight,
        uint256 _height,
        string memory _diagnosis,
        bool _isAdmitted
    ) public {
        patients[msg.sender] = Patient({
            name: _name,
            age: _age,
            gender: _gender,
            weight: _weight,
            height: _height,
            diagnosis: _diagnosis,
            isAdmitted: _isAdmitted
        });
    }

    function getPatientRecord(address _patientAddress) public view returns (Patient memory) {
        return patients[_patientAddress];
    }
    
    function updateDiagnosis(address _patientAddress, string memory _newDiagnosis) public onlyOwner {
        patients[_patientAddress].diagnosis = _newDiagnosis;
    }
}
