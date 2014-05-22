%% Signature generation algorithm for authenticating matrices U and V
function signature = signature_generation(U, V, key)

% Proposed algorithm
% 1. Sum the column of orthogonal matrices and create 1-D array
Usum = sum(U);  %GTR 22.05.14: C?ng t?ng t?ng c?t l?i -> ma tr?n 1 hàng, n c?t, các giá tr? ? m?i c?t= sum, ie. Usum=[1 2 3]
Vsum = sum(V);

% 2. Based on the threshold, map the array values into corresponding binary digits
Usum_threshold = median(Usum);  % threshold based on median value of each Uw & Vw matrix, l?y trung bình c?ng các c?t -> Usum_threshold=3, (1+2+3)/3=3
Vsum_threshold = median(Vsum);

% transform Usum martix to binary using above threshold
Usum(find(Usum > Usum_threshold)) = 1;
Usum(find(Usum < Usum_threshold)) = 0;

% transform Vsum martix to binary using above threshold
Vsum(find(Vsum > Vsum_threshold)) = 1;
Vsum(find(Vsum < Vsum_threshold)) = 0;

clear('Usum_threshold', 'Vsum_threshold');

% XOR the 2 matrices to obtain 1-D array of dimension 1x512
UV_XOR = bitxor(uint8(Usum), uint8(Vsum));

% 3. Generate a PSRNG sequence using the key of dim. 1x512 and XOR it with
%    the UV_XOR 1-D array above
rand('seed', key);
% produce binary sequence to perform XOR with UVsum
binary_seq = randi([0 1], 1, length(UV_XOR)); %GTR 22.05.14: randi(range, row,col) -> length(UV_XOR)=512 => t?o binary matrix 1x512
signature = double( bitxor(uint8(UV_XOR), uint8(binary_seq)) ); % signature length=512

clear('Usum', 'Vsum', 'UV_XOR', 'binary_seq');
end